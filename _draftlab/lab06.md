---
layout: lab
num: lab06
ready: false
desc: "Basics of electronics with Raspberry Pi"
assigned: 2018-08-22 08:45:00.00-7
due: 2018-08-25 15:45:00.00-7
starter-code-url: https://github.com/ucsd-cse-spis-2018/lab06-startercode.git
---

If you find typos or problems with the lab instructions, please report them on Piazza

# Learning objectives

In this lab you will be introduced to the basics of electronics using a a credit-card sized computer called the Raspberry Pi. You will build simple electronic circuits and write programs to control them. 

# Getting started

## Observe your Raspberry Pi
Take a look at the Raspberry Pi (or RPi for short) on your workbench. You are looking at the insides of a computer. Your gut feeling may be that it all looks very complex. Your premonitions are not misplaced. The circuit that you are looking at is not called the motherboard for nothing. 

The green base on which all the electronic components (which you see as bulgy entities) are laid out is a non-conductive substrate. This means that the green parts of the board don't conduct electricity. However, to connect the various electrical components, conductive tracks made of copper are etched on the green base. At the very center of your RPi sits a prominent black square block. This is the brain of your RPi: the processor (a 64-bit Quadcore ARM). On the back you'll find another black block, which holds 1GB of RAM (Random Access Memory). For now, just know that the RAM is a form of non-persistent memory. There are other components on the RPi. To identify them orient your RPi to match the circuit below.

<p align="center">
![RPi-3-modelB](/images/labs/images/RPi/rpi_pi3_detail.jpg){:height="400px"} 
</p>



Observe the components marked in this diagram on your RPi. 
We will focus on a few important components on the diagram:

1. Internet connectivity: The RPi can get Internet connectivity through the LAN port (Ehternet), or throught the built-in WiFi chip. In our setup, we will use the WiFi. 

2. USB ports: The RPi3 comes with four USB ports (older versions had fewer of these ports). We will use them to connect a mouse and keyboard. 

3. HDMI (High Definition Multimedia Interface) Video Output: This is an interface that connects your RPi to a monitor.

4. MicroSD card slot: All the software that runs on the RPi, which includes the Operating System (more on the OS later) as well as your programs, will be stored on the SD card that goes into the SD card slot. The SD card is essentially the Hard Drive of the RPi.

5. GPIO pins: This stands for General Purpose Input / Output. You won't be able to observe the GPIO pins on the Raspberry Pi on your workbench because they are hidden under the ribbon cable that connects them to the white breadboard. These pins can be configured to send/receive signals through your Python programs. You will control and sense the world around you through these pins.

6. Micro USB Power Input: Using this input you can power up your RPi using a wall charger or a battery. 

## Observe the connections from your RPi to other peripherals

In the setup provided to you, the RPi has been wired to work as a desktop computer. Actually, it's more than a desktop because it is set up to connect to an electronic circuit that you will soon create (something you can't do with standard desktops).
For the robotics projects, we will operate the RPi in an untethered fashion (so the robot can be mobile) but for now observe the following wired connections from the RPi to other peripherals:

* The RPi has a connection to a monitor via the HDMI port.
* The keyboard and mouse are connected via USB.
* The RPi is powered up using a charger that is plugged into the wall.
* The GPIO pins on the RPi are routed to a breadboard via a ribbon cable.

**Very important note: If you want to unplug anything from your RPi (keyboard, mouse, power cable, etc.) or plug anything into it, your RPi needs to be shut down (an exception is a USB thumb drive). Otherwise, you may damage the device. So when you start, you first connect all the peripherals and as a last step you plug in the power. When you want to unplug things, first shut the RPi down in software (select Shutdown under the raspberry icon in the menu bar) before removing anything.**

Now let's take a closer look at the breadboard and the GPIO breakout board that sits on it. You will need this information to complete the later exercises in this lab.


## The breadboard

The RPi chip itself is very small, so we will be attaching an electronic component called a breadboard  -- which is designed to make it possible to experiment with circuits by extending the available space.  For electricity to flow you need connections.  Think of a breadboard as a way of giving you more space to make those connections.  The main feature of the breadboard is that it comes with a set of in-built electrical connections which significantly simplifies the wiring involved in complicated circuits. Let's try to understand the electrical connections on the breadboard using the figures below:

<p align="center">
![RPi-desktop](/images/labs/images/RPi/breadboard.png){:height="400px"} 
</p>

The figure on the left shows a picture of the breadboard as visible to you, while the one on the right shows in internal electrical connections when the back of the breadboard is uncovered. The rows are numbered 1 through 30 and the columns 'a' through 'j'. In the figure on the right observe how the conductive metal strips run across the rows.  This means that any two grids that are on columns 'a' through 'e' are at the same *potential* as long as they are also on the same row. Similarly, any two grids that are on columns 'f' through 'j' are at the same potential as long as they are also on the same row. However, the two halves of a row are electronically disconnected.  As you will see, this helps you out a lot.

Are each of the following grids internally connected on the above shown breadboard?

* 1a and 2a
* 1a and 1b
* 1a and 2b
* 14c and 14f
* 1j and 2j
* 1a and 1e


Finally, the breadboard has two vertical lines running up and down on both sides.  The pins on each of these lines are electrically connected but the lines are electrically disconnected from each other. The convention is to connect a positive voltage (3.3V pin) to the line that has a '+' sign above it and connect the 'ground' (GND pin) to the line with the '-' sign above it.


## The GPIO pin numbering conventions

The Raspberry Pi 3, model B (which is the one we are using) has 40 GPIO pins that are laid out as two rows of 20 pins each, also depicted in the diagram below:

<p align="center">
![GPIO-numbering](/images/labs/images/RPi/RP3_Pinout.png){:height="400px"} 
</p>

The pins that are colored in orange are available for any general purpose and can be referred to and configured in your python programs. Some of these orange pins have an 'alternate function' as well; this means they may not be available if you are using that alternate function. In case you are not sure, avoid those pins and only use the orange colored ones that do not have an alternate function. There are two different conventions used to refer to these pins:

1. Physical location (board convention): One way is to just refer to the pins based on their physical location. These numbers are indicated in the gray boxes in the above diagram. All pins on the left half have odd number locations while all pins on the right half have even numbered locations.

2. BCM (broadcom convention): You can also use the broadcomm convention where the numbering is not based on the physical location. For example the pin at physical location 12 is referred to as pin number 18 (note that you drop the 'GPIO' part) as per the BCM convention.

Either of the above conventions is okay to use in your programs as long as you define which scheme you are using before you start referring to the pins.

Note that physical pins 1 and 17 provide 3.3V, while physical pins 2 and 4 provide 5V. Physical pins 6, 9, 14, 20 and 25 provide the ground (GND) signal which is also very important in your circuits.

The GPIO breakout board shown below makes all these pins available to you on a breadboard where you will be doing your electrical wiring.

<p align="center">
![GPIO-breakout](/images/labs/images/RPi/breakout.jpg){:height="300px"} 
</p>

The labels on the breakout board use the BCM naming convention. However, we have connected the breakout board in such a way that you can easily derive the physical pin number of any pin by looking at the row number that it is connected to on the breadboard. 


## Getting to know your desktop environment

<p align="center">
![RPi-desktop](/images/labs/images/RPi/desktop.jpg){:width="800px"} 
</p>

The operating system on the RPi is a version of Linux known as Raspbian. The picture above shows the Pixel desktop environment under Raspbian. Feel free to poke around and see what all of these icons mean.


### Terminal
Terminal is the command line interpreter. It is the icon on the top bar showing `>_`. Click it to open. You can also find it under the Accessories submenu of the main menu (the raspberry icon). 
When you open Terminal, notice the prompt says `pi@XXXX`. This means that you are user `pi` and the name of your machine is `XXXX`.
All the unix commands that you have learned so far can be used to navigate through the file system on your RPi. You can also use command line git just like how you would on the ieng6 machines.


### WiFi
You need to configure the on-board WiFi module with your credentials to be able to use the UCSD-Protected network. Open a Terminal window. Type the following command (this executes a script to set up the WiFi with your credentials; make sure you don't forget the `./`):

`./wifisetup.sh`

You should be prompted for your **wifi** username and password. Your RPi will automatically reboot. 
When it is done rebooting and you are back to your desktop environment, click the WiFi icon in the top right corner. It should indicate that you are now connected to the UCSD-Protected network.

While not necessary for this lab, if you want to know the IP address of your RPi, open a Terminal window and type:

`ifconfig`

It will show you a bunch of information, organized in three sections. In the bottom section, labeled `wlan0`, look for `inet addr`. The numbers that follow (something like 192.168.1.233) are your IP address. Knowing this will come in handy if you want to log in remotely using ssh.


## Create a git repo and get the starter code
Use your laptop or the RPi to create a new repo called `spis18-lab06-Name-Name`, for example using [Method 1](http://ucsd-cse-spis-2018.github.io/topics/github_create_repo/#method1). When creating the repo import the starter code from this git repo:  [{{ page.starter-code-url }}]({{ page.starter-code-url }}).

**Note that you must keep your git repo updated with the latest version of your code because your code will be erased from the RPi at the end of the lab session. This is to ensure that the hardware is ready for use by the next group. So don't forget to push your code to the online repo at the end of the lab, and preferably also a few times during the lab.**



## Set up your programming environment

* Configure your git credentials on the RPi. In the home directory `/home/pi` type the following commands replacing the name and email credentials with yours.

```
 git config --global user.name "Bert Sesame"
 git config --global user.email bsesame@eng.ucsd.edu

```

* Clone your git repo **over https** into your home directory on the RPi. DO NOT log into the ieng6 machines and try to do this step there. To clone your repo first open a browser on the RPi (or your laptop), and navigate to your repo on github which should be called `spis18-lab06-Name-Name`. Go to the green button that says 'clone or download' and get the https address of your repo. The **https address** should be something like `https://github.com/ucsd-cse-spis-2018/spis18-lab06-Name-Name.git`. Do not use the ssh address as you have in the past.

Make sure you have the starter code in your repo. If you did not import the starter code when creating the repo, ask the mentors for help.

In the terminal navigate to the your local git repo (~/spis18-lab06-Name-Name/ and open up idle by typing the following command

` sudo idle3 &`

As an alternative, you can also navigate to the repo using the file browser, right-click one of the .py files and select `Python 3 (IDLE)`. 
 
*A word on sudo*

You might be wondering why we use the word sudo to open idle. Unix / Raspbian has something known as *privileges*. This allows the operating system to prevent users from doing very powerful things (like destroying the operating system or attached devices) that could damage the system or compromise the security of other users.  It turns out that using the Python GPIO library is one such powerful thing.  You have to be a special user to run the library.  In order to get around this (in some cases) you can just tell the operating system, essentially, 'OK.  Look.  I know what I am trying to do here is very powerful and I need to be careful, so just let me do it.' This command to the operating system is 'sudo'. It stands for 'super user do'.  It is a command to Raspbian to go ahead and run a command that you don't really have privileges for, because you understand that it is very powerful, and you want to run it anyway. We use the word `sudo` to open idle3 because we will be soon running programs that use the Python GPIO library

You are now ready to start working on your first exercise where you will create your own circuit and control it using the starter code given to you. 



# Making an LED blink

In this exercise you will create a circuit consisting of an LED and a resistor connected to the RPi. You will then periodically blink the LED using the example program provided to you in the starter code.

**For all your work with Raspberry Pi, it is extremely important you do not make short circuit connections on the GPIO pins. A short circuit is when a supply or GPIO pin set to HIGH is directly connected to a GND or GPIO pin set to LOW. If you are unsure, ask a mentor or instructor to check your circuit before running your program. Always be extremely careful to avoid short circuits. It may corrupt the SD card or possibly even destroy the RPi.**


### Understanding the code

In IDLE3 open the file `01_blinking_LED.py`. Let's begin by trying to understand the given code.


The first two statements import the modules needed for this exercise:

``` 
import RPi.GPIO as GPIO
import time

```

The `RPi.GPIO` module provides routines for configuring the GPIO pins on the RPi and for sending and receiving signals on these pins. Since the GPIO pins are digital we can only send high or low voltages. 

The `time` module provides routines that make use of the clock on the RPi. Using the time module you can make the RPi wait for some time before executing the next python command in your program. For exmample, `time.sleep(0.5)` makes your program wait for half a second before moving on to the next line of code. 

The lines immediately after the import statements take care of configurations related to using the GPIO pins. The first one specifies that we are using the physical numbering scheme. 

```
GPIO.setmode(GPIO.BOARD) 
```

If we chose to use the BCM scheme, that line should be replaced by the following:
```
GPIO.setmode(GPIO.BCM) 
```

Before proceeding further, identify pin number 11 on your breadboard (remember, we are using physical numbering, so you will need to count the pins to find the location of pin 11). You will need this for wiring your circuit.

The Python GPIO library allows configuring certain pins to be either input or output pins using the `setup(Pin, mode)` function, where Pin is the pin number and mode is either GPIO.OUT (for output) or GPIO.IN (for input). If we want our program to generate high or low voltages on a pin that potentially drives other electronic components (such as LEDs or servos), then configure the pin to be an OUTPUT pin. If we want to read the signal generated by sensors into our program, then configure the pin to be an INPUT pin. 

In our code here, pin number 11 is configured to be an output pin using the command `GPIO.setup(LedPin, GPIO.OUT)`. It also sets the initial state of that pin to be LOW via the command `GPIO.output(LedPin, GPIO.LOW)`.

After these inital settings and definitions comes the main program. For now ignore the try ...except structure. The key part of the code is the `while True:` loop. The code in this loop contains the main functionality and runs forever. Any ideas why we are doing this?


### Wiring the circuit 

To create the circuit you will need the following components

* One LED (any color)
* Two wires
* One 100 ohm resistor (the resistor with bands colored brown, black, black, black, brown or something similar). The colored bands on the resistor encode the resistor value. A good explanation of how to decipher this code is given on this [website](https://www.wikihow.com/Read-Axial-Lead-Resistors).

 
The picture of an LED and the symbol used for it in circuits is shown below:

<p align="center">
![RPi-desktop](/images/labs/images/RPi/LED.jpg){:height="200px"} 
</p>

The longer leg of the LED is called the 'anode' and the shorter leg is called the 'cathode'. When there is a positive voltage difference between the anode and the cathode, the LED is forward biased or "on state" and current flows through the circuit lighting it up, otherwise the LED is in the "off state". 

Wire up the circuit shown by the following diagram. Remember: we are using physical pin numbering for the RPi. You should use jumper wires and the breadboard to make the physical connections. 

<p align="center">
![RPi-desktop](/images/labs/images/RPi/schematic_led.jpg){:height="150px"} 
</p>

Ask an instructor or mentor is you don't understand the diagram. For a more in depth information on configuring GPIO pins as outputs refer to [this website](https://www.raspberrypi.org/documentation/usage/gpio-plus-and-raspi2/).

Now, run the `01_blinking_LED.py` program. Hopefully you should have a blinking LED. If you were unsuccessful, the problem is most likely with your wiring. If you were successful, take a close look at the code. 

Now, modify the program (and rename it to `01_blinking_LED_sol.py`) to double the frequency at which the LED blinks. Make sure you commit this code to your github repo.



# Controlling an LED using a button

Next, we are going one step further and we'll use a button to control the LED. You don't need to undo the wiring you already created for the previous problem. This can stay the same. We will just add circuitry for a button.

Buttons are switches that are used to connect or disconnect circuits. In the figure below, pins pointed out by the arrows of the same color are internally connected. When the button is pressed, the pins indicated by the blue arrow will connect to the pins indicated by the red arrow.


<p align="center">
![RPi-desktop](/images/labs/images/RPi/button.png){:height="150px"} 
</p>

### Understanding how to use a button 

Now, let's start wiring the circuit. You should keep the LED circuit from the precious exercise. Then add the button as per the circuit diagram below.

<p align="center">
![RPi-desktop](/images/labs/images/RPi/schematic_button.jpg){:height="100px"} 
</p>


Next, open the program `02_buttonLED.py` in IDLE3. One of the key differences in this exercise compared to the previous one is that you will configure the pin connected to the button as an INPUT pin. Here is a nice excerpt from [a website](http://blmrgnn.blogspot.com/2016/02/gpio-general-purpose-inputoutput-inputs.html) explaining such a configuration:

*A GPIO pin configured as an input is used to read (to input) the value of one digital signal.  In this case the pin is converting the voltage being delivered to the pin into a logical value of 0 or 1 for subsequent use in the program.  By convention, when the voltage on the pin is 'high' (near Vcc), reading the pin will result in reading a logic 1, while when the voltage is 'low' (near GND), reading the pin will result in reading a logic 0.*

So, the bottom line is that when we configure a GPIO pin as an input, we can read the voltage at that pin in our Python program. 

But, what is the expected voltage if the pin is not connected to anything at all? This would occur in the button circuit we just built and the button is not pressed. The answer is that we really can't say. When a GPIO pin is set as an input but is not connected to anything it is 'floating' and has no defined voltage level. For us to be able to reliably detect whether the input is high or low, we need to tie it so that it is always connected to something and either reads high or low. This can be done by using a pullup resistor, as shown in the diagram below. (If you are interested in exactly how this work, you can ask the instructors).

<p align="center">
![RPi-desktop](/images/labs/images/RPi/schematic_button_pullup.jpg){:height="200px"} 
</p>

However, you don't actually have to wire up a separate resistor in your circuit. Instead, the RPi has these pullup resistors internally built-in. You just have to specify in the software that you would like to use it. In the code, you will find the line: 

```
GPIO.setup(BtnPin, GPIO.IN, pull_up_down = GPIO.PUD_UP) 
```

This makes the BtnPin an input AND internally attaches the pullup resistor. Note that pulldown resistors are available as well. If you want to specify a pin as simply an input, without the pullup or pulldown resistor, you can write:

```
GPIO.setup(Pin, GPIO.IN) 
```

Now, let's have a closer look at the starter code. This program polls pin 15 (the pin connected to the button) and prints the status of that pin (1 indicates True or high voltage, 0 indicates False or a low voltage). It doesn't do much more than that at the moment. You will need to modify the code so that the button presses control the led. However, before you do this, try to understand the starter code first. What do you expect the output to be?

Run the code. What do you get? Come up with a simple test to check the correctness of the program. 

### Controlling the LED

Now, it's time to write some code of your own.

(1) Modify the program such that the LED is ON when you press the button and OFF when you don't press the button. Name it `02_buttonLED_sol1.py` and commit it to the github repo.

(2) Now change the functionality: toggle the LED every time the button is pressed. So, if the LED is ON and the button is pressed, it should turn OFF. If the LED is OFF and the button is pressed, it should turn ON. So pressing the button changes the state of the LED, from ON to OFF to ON to OFF etc. This functionality is trickier to obtain. You will need to think carefully how you can accomplish this. Name this version of your code `02_buttonLED_sol2.py` and commit it to the github repo.


# Controlling a servo motor

A servo is an electrical motor that comes with built-in control circuitry. There are two types of servos: standard servos and continuous rotation servos. In this lab, we will be working with standard servos. A stardard servo can move its arm half a rotation, from an angle of 0 degrees to an angle of 180 degrees. Servos are used in a lot of applications, for example to control flaps and rudders of RC aircraft or rotate camera turrets.

Keep the circuitry from the previous problems, and add a servo. The wiring is shown in the diagram below.
<p align="center">
![RPi-desktop](/images/labs/images/RPi/schematic_servo.jpg){:height="200px"} 
</p>

### Testing the servo 

Now look at the starter code for the servo in `03_servo.py`. The first few lines of code should look familiar to you: we are configuring pin 7 as an output as it will be used to control the servo. However, the control signal we will send to the servo is a PWM or Pulse Width Modulation signal. What this means is that it alternates between HIGH and LOW at a certain frequency. The percentage of time the signal is HIGH is called the duty cycle. By changing this duty cycle, we can signal to the servo to which angle we want it to move. 

The program includes code between the comments `#--- Start of the PWM setup --- ` and `#--- End of the PWM setup --- ` that takes care of this signaling. It is not important to understand the details here. Just leave the code as is and realize that it takes care of the PWM signal generation. The only thing you really need to know is that it defines a function `set_duty_cycle(angle)`. This function generates the PWM signal to tell the servo to move to the position indicated by 'angle' (between 0 and 180).

Try out the starter code. You should see the servo move between positions 0 and 180.

You will notice that the `pwm_servo.start()` command tells the servo to *start* moving to the new angle. The actual motion will take some time. This is why there are the  `time.sleep()` commands: we want to halt the code execution long enough so that the servo can move to its desired destination.

What happens when you reduce the sleep time? Try decreasing it to 0.8 seconds, 0.5 seconds, 0.1 second, etc. Can you explain what you observe?


### Modifying how we implement delays 

Next, open the starter code in `04_timing.py`. This shows an alternative way for a program to delay execution without explicitly adding in sleep time with time.sleep(). Execute the code to verify its functionality. It prints a comment every second, but the way this delay is implemented is much more flexible than when using time.sleep(). Can you see why?

Now, let's use this knowledge to improve the servo example code. These last two coding assignments are not easy and will challenge your ability to think about real-time coding. If you are sturggling, don't despair. Part of the goal is to realize the challenges that result from dealing with the concept of time in embedded systems. Thinking about functionality as a collections of states (as in Picobot. Remember that lab?) is very useful here. We also discuss this more in lecture. Just give it a shot and see what you can come up with.

(1) Modify the code from `03_servo.py` to perform the same functionality, but without using time.sleep(). Instead, use the technique shown in `04_timing.py`. Name this version of your code `03_servo_sol1.py` and commit it to the github repo.

(2) Now, let's modify the functionality a bit. The way you rewrote your code in part (1) will allow you to do this. We want the servo to move as we did before, but we also add a button. *As soon as* the button is pressed, the servo should move back to position 0 and stay there as long as the button is pressed. Why would this be hard to implement if you use time.sleep()? Name this version of your code `03_servo_sol2.py` and commit it to the github repo. 



# [Optional] Trying out the camera and other sensors

If you are interested, we have a lot of other sensors available for you to try out. Ask one of the instructors or mentors. They can give you the hardware, wiring diagrams and sample code to try them out. We have distance sensors, light sensors and a camera. The camera is especially interesting as it allows you to now apply the image processing you've learned, to real-time processing of video streams.


 
