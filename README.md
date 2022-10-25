# Q1 notebook
this is the note book for the first quarter of DE Engeneering 3



## projects 

### code and circuits

* [circuitPython](#CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython_sensor](#CircuitPython_sensor)
* [ButtonCounter_LCD](#ButtonCounter_LCD)
---

### cad
* [Swingarm](#Swingarm)
* [Pullcopter](#pullcopter)
* [cilinder](#cilinder)

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




# ButtonCounter_LCD

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






# Swingarm
this was a CAD assignment that was pretty difficult because not all of the demetions are listed and you need to find them out one at a time and sometime put in a number you know isnt correct.  
Here are some pictures of the project

![Screenshot 2022-10-18 150344](https://user-images.githubusercontent.com/71406784/196520985-bd7c9522-75ee-4059-bc15-e2cd047fdabb.png)



![Screenshot 2022-10-18 150327](https://user-images.githubusercontent.com/71406784/196520997-0a1ae627-575b-4ae6-b67a-99874fc9e193.png)


and here is my project:


![Screenshot 2022-10-18 150305](https://user-images.githubusercontent.com/71406784/196521011-b802d479-ca41-4d92-b144-398aa1dc8997.png)

this one was difficult because it was my first time i had done anything like this and so next time i will be better equiped to handle it. The most important thing is to plan ahead and put time into doing things right in the begging so you dont have problems later on. 


# pullcopter
This on we worked in pairs to creat a small helecotper toy in cad, it work by pulling of a "key" in order to get the "copter" part to spin and create lift.
this was not all to difficult as we were givin each step in order, the difficult part was working together with another person, this was not a problem for me asjosh bleakley worked well together.
### parts
here is the "key":
![Screenshot 2022-10-24 153014](https://user-images.githubusercontent.com/71406784/197609850-1afa6c1d-f26d-4d49-b20f-bed6d7c2673e.png)
![Screenshot 2022-10-24 153031](https://user-images.githubusercontent.com/71406784/197609896-90f3158c-ab18-4288-98d7-b177abeda48c.png)

here is the base(top and bottom):

![Screenshot 2022-10-24 153224](https://user-images.githubusercontent.com/71406784/197610294-f32654e8-0422-47ef-afe3-52a00e26f35f.png)
![Screenshot 2022-10-24 153251](https://user-images.githubusercontent.com/71406784/197610302-5a8df241-ce2c-4501-be90-4502de38095f.png)
![Screenshot 2022-10-24 153316](https://user-images.githubusercontent.com/71406784/197610313-4237c5ad-8640-4bdb-a083-4b2d467ccc0d.png)

here is the "spinner":

![Screenshot 2022-10-24 153434](https://user-images.githubusercontent.com/71406784/197610542-36d5889b-9dc4-4c9f-a756-8d67b2453d81.png)

here is the prop:

![Screenshot 2022-10-24 153456](https://user-images.githubusercontent.com/71406784/197610609-fc50d5fe-0636-4c2e-8918-b0d22866d70c.png)

### complete

![Screenshot 2022-10-24 153804](https://user-images.githubusercontent.com/71406784/197611040-2abb28bc-5a14-4cdd-9a82-80036e79d458.png)

### reflection
This wasnt to hard of a project because it wasn't a ton of work of especially difficult.The trick was team work and prexisting cad knowledge.
here is the document we worked on:https://cvilleschools.onshape.com/documents/c21ea5d854d718a86e6eb309/w/f28e1c984dc3fe65682f78f2/e/60f084a7ede173a9bd13a529


# cilinder
this was a cad project for which we needed to correctly mesure the mass and other parts of the design. we needed to make it in a way so that we could change dementions of a part and and have it still work.
This required a lot of cad skill and knowledge 
Here are some pictures from various different final pieces 

![Screenshot 2022-10-20 152149](https://user-images.githubusercontent.com/71406784/197039289-f7721daf-ddf9-4b23-84c7-3bc77117e05f.png)

![Screenshot 2022-10-20 152109](https://user-images.githubusercontent.com/71406784/197039301-f3d3c183-0052-4f5b-ba10-abf90ebb0e0e.png)

![Screenshot 2022-10-20 151917](https://user-images.githubusercontent.com/71406784/197039309-ab076236-4df8-412e-a40a-db3ead918f97.png)

the problems of this for me was mainly procrastination as i had the skills to do every thing but it looked imposing to start. Next time i will just start and go.


