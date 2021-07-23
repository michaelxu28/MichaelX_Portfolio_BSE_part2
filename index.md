# Hand Wash Timer
 This project is a hand wash timer that counts to twenty seconds every time you wash your hands. It uses a ultrasonic sensor to detect movement 30 cm away to start the timer. The timer is displayed on a OLED display. The project also includes a LCD display which shows the current time, date, and temperature, and a speaker that plays audio from a SD card to encourage sufficient hand scrubbing. 
 
Resources:
------
[Hand Wash Timer](https://create.arduino.cc/projecthub/the-tech-lab/fight-coronavirus-simple-handwash-timer-4dc8ac).  

[Ultrasonic sensor](https://howtomechatronics.com/tutorials/arduino/ultrasonic-sensor-hc-sr04/).  
[LCD display](https://www.instructables.com/Arduino-Interfacing-With-LCD-Without-Potentiometer/). 
[RTC](https://howtomechatronics.com/tutorials/arduino/arduino-ds3231-real-time-clock-tutorial/). 
[OLED display](https://create.arduino.cc/projecthub/infoelectorials/project-011-arduino-1-3-i2c-white-oled-display-project-a547d4).  
[Speaker and SD card](https://www.c-sharpcorner.com/article/audio-play-using-sd-card-module-and-arduino/).  
 
| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Michael | Lynbrook HS | Electrical Engineering | Incoming Junior


![image](https://user-images.githubusercontent.com/71350303/126834812-36acd159-99f5-44a2-ac9d-1452128f295c.jpeg)

  
# Demo Video: 
[![Demo Video](https://cdn.discordapp.com/attachments/501260125731028994/862438682706313256/Screen_Shot_2021-07-07_at_2.03.13_PM.png )](https://www.youtube.com/watch?v=AGEDjoDWGVE "Demo Night Video"){:target="_blank" rel="noopener"}

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

