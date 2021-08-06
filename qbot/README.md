# qbot

https://github.com/LoisLab/qbot

Build a Self-Driving Q-Bot using a Raspberry Pi Zero-W

Here is an overview of the project: https://medium.com/@michael_87060/build-a-self-driving-q-bot-6aa67ba60769

(and here is an older repo that supports a BeagleBone Blue: https://github.com/jvon-challenges/qbot)

The Q-bot is a small robot and associated software that uses machine learning (specifically Q learning) to learn how to complete a simple task (eg, seek the nearest object in its surroundings). The training can take place in a virtual or physical environment.

The build should cost <$50 with readily-available parts, and less if you salvage. The physical robot uses a Raspberry Pi Zero W, a Sparkfun VL53L1X laser time-of-flight sensor, and 28byj geared stepper motors for movement.  Aside from assorted nuts and bolts, a battery, and some wires, the only other required components can be 3D printed.  Links are provided below to the components you will need.  These are example products or vendors only; feel free to substitute parts wherever you like.  We are not endorsing, sponsored by,  or recommending any particular seller.

- Raspberry Pi Zero W: 
https://www.adafruit.com/product/3708

- 28byj Steppers with drivers: 
https://www.amazon.com/dp/B06X982PSL

- VL53L1x ToF distance sensor:
https://www.sparkfun.com/products/14722

- M3 hardware assortment:
https://www.amazon.com/gp/product/B07CZBR66J

- F to F dupont wires:
https://www.amazon.com/dp/B07GD2BWPY

For power, any small USB battery pack will be enought to run the bot. I used a 2S lipo 
battery and a BEC (battery eliminator) because I had them on hand for other projects, but
a small flat USB power bank is probably easier because no special charger is needed.

- USB battery pack:
https://www.amazon.com/dp/B076HJTNYJ/

- 2S lipo example:
https://www.amazon.com/dp/B07BJZZYBY

- BEC example: 
https://www.amazon.com/gp/product/B074PM59YS/

A video walkthrough of the build can be found here: https://youtu.be/-1W7-Q0RIaM

There are three example files included in this repo:

- example_virtual.py will create an instance of a virtual Q-bot and it will train to seek a randomly-generated virtual obstacle.  This example does not require a physical q-bot; you can run this on your laptop or desktop and it will render the virtual bot and its obstacle on screen using the python 'turtle'.

- example-physical.py will attempt to train the physical q-bot by looking around for an obstacle and learn to move closer to it by trial and error, improving as it goes

- example_virtual_physical will create a virtual q-bot, train it in software, and then use the learned Q-table values from the software training to have the physical Q-bot seek its nearest obstacle 

Enjoy the project files, and please reach out to us with questions, comments, and stories about your work with this project!  We can't wait to hear from you.

For hardware: jeff@loislab.org
For software: michael@loislab.org
