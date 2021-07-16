# Hand Wash Timer
 This project is a hand wash timer that counts to twenty seconds every time you wash your hands. It uses a ultrasonic sensor to detect movement 30 cm away to start the timer. The timer is displayed on a OLED display. The project also includes a LCD display which shows the current time and date, and a speaker that plays audio to encourage sufficient hand scrubbing. I will also maybe include a temperature sensor but no promises. 
 
| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Michael Xu | Lynbrook HS | Electrical Engineering | Incoming Junior


![Headstone Image](https://www.webstaurantstore.com/images/products/extra_large/569254/2102974.jpg)
  
# Demo Video:
[![Demo Video](https://cdn.discordapp.com/attachments/501260125731028994/862438682706313256/Screen_Shot_2021-07-07_at_2.03.13_PM.png )](https://www.youtube.com/watch?v=AGEDjoDWGVE "Demo Night Video"){:target="_blank" rel="noopener"}
# Code for the Project:  
https://github.com/michaelxu28/Cat-Laser   

# Final Milestone
my final milestone was soldering the wires to a perfboard. The arduino only has two ground ports, and my project needed four, so I connected three of the wires to one rail of the perfboard. I did the same with the 5v port and used the second ground port for the laser. Finally, I switched the button with a analog joystick. The joystick is used to control the servos and it even has a built-in button, which allows me to turn on and off the laser. 

[![Final Milestone](https://cdn.discordapp.com/attachments/501260125731028994/862438682706313256/Screen_Shot_2021-07-07_at_2.03.13_PM.png )](https://www.youtube.com/watch?v=ookglHMfglg "Final Milestone"){:target="_blank" rel="noopener"}

# Second Milestone
my second milestone was finishing a working cat laser turrent. One servo is connected to the arm of the second, and the laser is mounted on the arm of the top servo. When the button is pressed, two servos move in random directions and the laser turns on. The bottom servo allows the laser to move left and right while the top servo moves it up and down.  
  
      
            
            
[![Second](https://cdn.discordapp.com/attachments/501260125731028994/862438682706313256/Screen_Shot_2021-07-07_at_2.03.13_PM.png)](https://www.youtube.com/watch?v=328fONESxTU "Second Milestone"){:target="_blank" rel="noopener"}
# First Milestone
  
My first milestone was getting the ultrasonic sensor to work and track distance in cm. The ultrasonic sensor sends out a sound wave and calculates the distance it takes for the sound wave to travel and reflect back. Whenever the distance is less than 30 cm, it turns on a led and sends a message to the serial output. This allows me to turn on my 20 second timer every time I wave my hand around the sensor. Instead of putting the timer on the serial, I put it on a LCD display. 
[![First Milestone](https://cdn.discordapp.com/attachments/501260125731028994/862438682706313256/Screen_Shot_2021-07-07_at_2.03.13_PM.png)](https://youtu.be/UzFh56dkveo "First Milestone"){:target="_blank" rel="noopener"}
