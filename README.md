# Q1 notebook
this is the note book for the first quarter of DE Engeneering 3



## projects 

### code and circuits

* [circuitPython](#CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython_sensor](#CircuitPython_sensor)
* [ButtonCounter_LCD](#ButtonCounter_LCD)
---



## CircuitPython_Servo

### for this project we just needed to make a servo turn  using python
this project was very simple as it was the one of our first project of the year so all we needed was the arduino and the computer and the servo 
here is the code i used:
```python
import time  #importing all the things
import board
import pwmio
from adafruit_motor import servo

pwm = pwmio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50) # this is where we set of the code


my_servo = servo.Servo(pwm) #defining my serco 

while True:
    for angle in range(0, 180, 5):  # tells it how fast to go and where to stop
        my_servo.angle = angle
        time.sleep(0.05) # pauses it for a second 
    for angle in range(180, 0, -5):  # same code just with the values to turn it around            
        my_servo.angle = angle
        time.sleep(0.05)

```

### Evidence


### Wiring
![download](https://user-images.githubusercontent.com/71406784/192608178-834fa94a-b170-454e-8a54-c0727bf4316f.png)

### Reflection

I didnt have any real problems this project, just had to set up all the wires and the servo in code



## CircuitPython_sensor

### Description & Code

```python
  import time #huge thanks to gaby for help on this code
    import board
    import adafruit_hcsr04
    import neopixel
    import simpleio

    sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D6)   # creating sonar variable
    dot = neopixel.NeoPixel(board.NEOPIXEL, 10, brightness=0.5) # creating dot variable 

    r = 0  # setting my three colors ints to 0
    g = 0
    b = 0


    while True:

    try:
        distance = sonar.distance # setting the variables
        print((distance))

        if distance < 5: # start of if statement if distance is less than f then set the color vaiables to red
            r = 255 # acitivated variable
            g = 0
            b = 0
        elif distance > 5 and distance < 20: # this else statement creates the second color preset
            r = simpleio.map_range(distance, 5, 20, 255, 0) # set up the distance color conection
            b = simpleio.map_range(distance, 5, 20, 0, 255) # set up the distance color conection
            g = 0 
            r = int(r)   # ints set up
            g = int(g)
            b = int(b)
        elif distance > 20 and distance < 35: # this else statement creates the second color preset
            r = 0
            b = simpleio.map_range(distance, 20, 35, 255, 0)  # acitivated variable with the var distance to get blue and green going 
            g = simpleio.map_range(distance, 20, 35, 0, 255)
            r = int(r)
            g = int(g)   # ints set up
            b = int(b)
        elif distance > 35:  #else if for > than 35
            r = 0    #  vars  set to pure green if its out side the range we want
            b = 0
            g = 255
            r = int(r)
            g = int(g)
            b = int(b)
        print(r, g, b)  # prints the color variables to show us the color in code
        time.sleep(0.05)

    except RuntimeError:  # gives us simple error message if it doesn't work 
        print("Retrying!")
        r = 0
        g = 0
        b = 255
        time.sleep(0.1)

    print(r, g, b)  
    dot.fill((r, g, b)) # tells the dot variable what to do
    time.sleep(0.05) # delay so code don't break
```

### Evidence

here is a video.


https://user-images.githubusercontent.com/71406784/191340307-837a51d7-b6ea-4963-bc91-7a316856a9d1.mp4


### Wiring
 This is the wiring diagram:
 ![Screenshot 2022-09-19 151305](https://user-images.githubusercontent.com/71406784/191097368-cd9934de-e873-4235-b3da-187033846d88.png)
 
### Reflection

This project took focus and time to complete and the consistant problem of getting the correct file to the right place in my computer. the code for this is long but not overly complex. I would in the future write my code better and study the concepts of loops and color theor a bit more. 




#ButtonCounter_LCD

#### this was a bit more dificult than the earlier assignments but over all not too complex as I had done this before last year. I have the wiring diagram from online.
```python
import board
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
from digitalio import DigitalInOut, Direction, Pull # set up code

# get and i2c object
i2c = board.I2C()       # button set up 
btn = DigitalInOut(board.D3) 
btn.direction = Direction.INPUT
btn.pull = Pull.UP
# some LCDs are 0x3f... some are 0x27.
lcd = LCD(I2CPCF8574Interface(i2c, 0x27), num_rows=2, num_cols=16) # lCD set up 
cur_state = True  # setting up boolean 
prev_state = True
buttonPress = 0

while True: # basic while loop
    cur_state = btn.value  # setting button to current state
    if cur_state != prev_state:  # if statment for button press
        if not cur_state:      # if not current position 
            buttonPress = buttonPress + 1  # counts 
           lcd.clear()                     # clears laps message
            lcd.set_cursor_pos(0, 0)  # cursor position
            lcd.set_cursor_pos(1, 0)
            lcd.print("BTN Press:")  # displays btn press on lcd
            lcd.print(str(buttonPress))
        else:
            lcd.clear()  # clears lcd 

    prev_state = cur_state  # closes while loop
```


### Wiring
![increment-decrement-counter-arduino-1024x585](https://user-images.githubusercontent.com/71406784/192609663-81f87442-9b0f-44db-a81c-4deeca209c86.png)

### Reflection
this wasnt too hard as i have done it before but i want to thank Anton for help on the code. i have already done a reflection on this last year.

