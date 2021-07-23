# Hand Wash Timer
 This project is a hand wash timer that counts to twenty seconds every time you wash your hands. It uses a ultrasonic sensor to detect movement 30 cm away to start the timer. The timer is displayed on a OLED display. The project also includes a LCD display which shows the current time, date, and temperature, and a speaker that plays audio from a SD card to encourage sufficient hand scrubbing. 
 
#### First session portfolio
[Cat Laser](https://michaelxu28.github.io/BSE-MichaelX-Portfolio/)  
 
Resources:
------
[Hand Wash Timer](https://create.arduino.cc/projecthub/the-tech-lab/fight-coronavirus-simple-handwash-timer-4dc8ac)  
[Ultrasonic sensor](https://howtomechatronics.com/tutorials/arduino/ultrasonic-sensor-hc-sr04/)   
[LCD display](https://www.instructables.com/Arduino-Interfacing-With-LCD-Without-Potentiometer/)  
[RTC](https://howtomechatronics.com/tutorials/arduino/arduino-ds3231-real-time-clock-tutorial/)  
[OLED display](https://create.arduino.cc/projecthub/infoelectorials/project-011-arduino-1-3-i2c-white-oled-display-project-a547d4)   
[Speaker and SD card](https://www.c-sharpcorner.com/article/audio-play-using-sd-card-module-and-arduino/)  
 
| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Michael | Lynbrook HS | Electrical Engineering | Incoming Junior


![image](https://user-images.githubusercontent.com/71350303/126834812-36acd159-99f5-44a2-ac9d-1452128f295c.jpeg)

  
# Demo Video: 
[![Demo Video](https://cdn.discordapp.com/attachments/501260125731028994/862438682706313256/Screen_Shot_2021-07-07_at_2.03.13_PM.png )](https://www.youtube.com/watch?v=AGEDjoDWGVE "Demo Night Video"){:target="_blank" rel="noopener"}

# Code:
```cpp
#include <LiquidCrystal.h>
#include <DS3231.h>
#include "U8glib.h"
#include <TMRpcm.h>
#include <SD.h>

#define SD_ChipSelectPin 10
TMRpcm tmrpcm;

DS3231 rtc(SDA, SCL);
U8GLIB_SH1106_128X64 u8g(U8G_I2C_OPT_NONE);  // I2C / TWI 

LiquidCrystal lcd(A1, A2, 5, A3, 3, 2); // 4 = A3 12 = A1 11 = A2
int trigPin = 7;
int echoPin = 8;
int textpos = 0;
long duration;
int distance;

const unsigned char hands [] PROGMEM = {
  //bitmap for hands pic
};

const unsigned char water [] PROGMEM = {
  //bitmap for water pic
};

void setup() {
  tmrpcm.speakerPin = 9;
  SD.begin(SD_ChipSelectPin);
//  if(!SD.begin(SD_ChipSelectPin)){
//    Serial.println("sd doesnt work");
//    return;
//  }
  rtc.begin();
  analogWrite(6, 75);
  lcd.begin(16, 2);
  pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPin, INPUT); // Sets the echoPin as an Input

  //Serial.begin(9600); // Starts the serial communication
}

void loop() {
  //scrolling text for oled display
  u8g.firstPage();  
  do {
    draw2(textpos);
  } while( u8g.nextPage() );
  textpos = textpos + 7;
  
  lcd.setCursor(0, 0);
  
  lcd.print(rtcinfo());
  delay(500);
  
  lcd.scrollDisplayRight(); // scrolls right and for each scroll it keeps track of the og position
  digitalWrite(trigPin, LOW);

  //code for ultrasonic sensor
  delayMicroseconds(2);
  // Sets the trigPin on HIGH state for 10 micro seconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  // Reads the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);
  // Calculating the distance
  distance = duration * 0.0343 / 2;
  if (distance > 0 && distance <= 30) {
    //Serial.print("less than 30 cm ");
    draw1();
    
  }
  
  Serial.print("Distance: ");
  Serial.println(distance);
}

String rtcinfo(){
  //flawless rtc clock code that never fails 
  String time = rtc.getTimeStr();
  String first = time.substring(0,2);
  int hour = first.toInt();
  String amorpm = "am";
  if(hour > 12){
    amorpm = "pm";
    hour = hour - 12;
    if(hour >= 10){
      first = String(hour);
      if(hour = 12){
        amorpm = "pm";
      }
    }
    else{
      first = "0" + String(hour);
    }
  }
  time = time.substring(2,5);
  String date = rtc.getDateStr();
  String months[] = {"Jan" , "Feb" , "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep" , "Oct" ,"Nov" , "Dec"};
  int month = date.substring(3,5).toInt();
  month = month - 1;
  String dateoutput = months[month] + " " + date.substring(0,2);
  //int temp = rtc.getTemp();
  //int tempinF = (temp * 1.8) + 32.0;
  
  String output = "Date: " + dateoutput + " Time: " + first + time + amorpm ;
  //Serial.print(output);
  return output;
}
// draws the hands
void draw(void) {
  // graphic commands to redraw the complete screen should be placed here  
  u8g.drawBitmapP( -23, 0, 16, 64, hands);  /// 16, 64 for a 128x64 image
}

//draws the water droplets
void drawwater(int x) {
  u8g.drawBitmapP(10, x , 8, 64, water);
}

//draws the timer for 20 seconds and also calls the droplet code to 
// also draw the droplets AND ALSO MAKES THE SPEAKER PLAY A RANDOM SONG FOR 20 SECONds
void draw1(void) {
  tmrpcm.setVolume(5);
  int x = random(1,5);
  String y = String(x) + ".wav";
  char uwu[6];
  y.toCharArray(uwu,6);
  tmrpcm.play(uwu);
  int position = 0;
  for(int i = 20; i >= 0; i --){
    
    u8g.firstPage();
    do{
      //drawwater(0);
      drawwater(position);
      drawwater(position - 75);
      drawwater(position - 150);
      u8g.setFont(u8g_font_helvR12);
      u8g.setPrintPos(80, 20);
      u8g.print("Timer: ");
      u8g.setFont(u8g_font_freedoomr25n);
      u8g.setPrintPos(80, 50);
      u8g.print(i);
    }while(u8g.nextPage());
    lcd.scrollDisplayRight();
    delay(500);
    lcd.scrollDisplayRight();
    delay(500);
    position = position + 5;

  }
  tmrpcm.play("alarm.wav");
}

/// draws the demeaning text and also calls draw to draw the hands
void draw2(int pos){
  pos = pos + 15;
 
  draw();
  u8g.setFont(u8g_font_9x15B);
  u8g.setPrintPos(80, pos);
  u8g.print(":)");
  pos = pos + 30;
  u8g.setPrintPos(80, pos);
  u8g.print("DIE");
  pos = pos + 30;
  u8g.setPrintPos(80, pos);
  u8g.print("WILL");
  pos = pos + 30;
  u8g.setPrintPos(80, pos);
  u8g.print("YOU");
  pos = pos + 30;
  u8g.setPrintPos(80, pos);
  u8g.print("OR");
  pos = pos + 30;
  u8g.setPrintPos(80, pos);
  u8g.print("HANDS");
  pos = pos + 30;
  u8g.setPrintPos(80, pos);
  u8g.print("YOUR");
  pos = pos + 30;
  u8g.setPrintPos(80, pos);
  u8g.print("WASH");
}
```
# Final Milestone
My last milestone was adding a speaker and SD card module to my project. The SD card module reads an SD card, which contains audio files, to the arduino and allows the speaker to play these files. The files have to be in wav format (PCM unsigned 8 bit 16k hz) and are played through the speaker with a transistor acting as a amplifier. The amplifier increases the speaker signal so it actually plays audible sound. Whenever the hand wash timer starts, the speaker plays a random 20 second audio file I downloaded and plays a alarm at the end. 

[![Final Milestone](https://cdn.discordapp.com/attachments/501260125731028994/862438682706313256/Screen_Shot_2021-07-07_at_2.03.13_PM.png )](https://www.youtube.com/watch?v=ookglHMfglg "Final Milestone"){:target="_blank" rel="noopener"}

# Second Milestone
My second milestone was first adding scrolling text to my LCD display, which allows me to have more than 16 characters per line. For the first line on the LCD, I put the info for the current date, time, and measured temperature. This data is recieved from the RTC sensor, which keeps track of the time and date and also can measure the temperature. However, the LCD cannot display scrolling text and a timer at the same time, which was why I added a second OLED display for the timer. The OLED can also display image bitmaps, so I took the time to add some threatening text and some pictures of hand washing. 
  
      
            
            
<iframe width="560" height="315" src="https://www.youtube.com/embed/In7Fj0EMY_E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# First Milestone
  
My first milestone was getting the ultrasonic sensor to work and track distance in cm. The ultrasonic sensor sends out a sound wave and calculates the distance it takes for the sound wave to travel and reflect back. Whenever the distance is less than 30 cm, it turns on a led and sends a message to the serial output. This allows me to turn on my 20 second timer every time I wave my hand around the sensor. Instead of putting the timer on the serial, I put it on a LCD display. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/wI0pApb0Pbo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Circuit (1st milestone)

<img width="1071" alt="Screen Shot 2021-07-16 at 2 00 51 PM" src="https://user-images.githubusercontent.com/71350303/126830853-d9856f7a-f536-41e3-8fd0-1b03d35aabad.png">

