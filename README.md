# bfc3000
##Watch and analyze your bird's eating habits
![Schematics](https://github.com/barde/bfc3000/raw/master/overview.png)

###Aim 
Writing a database over multi week time frames. Timestamped entries are written by wild bird's setting off an metal
touch sensor.

###Hardware hacks

####Parasitic casing and power source

Gut the solar LED lamp and solder a connector for easy access from the step up converter to 5V.
As the sensors utilize 5V I keep the power on two separate rails on my perfboard.

####Connector on base board

The OpenLog and TinyRTC modules are plugged directly from their female header into a male socket. This puts stability
and reduces cable clutter in the case.

####ICSP header

Even the small space on the board leaves some place for a 6 pin ICSP connector for later reprogramming.

###Used hardware
|Hardware|Note|Price|My Source|
|--------|-----------|----:|------|
|PIR sensor|low active so possible to mock with a push button |$1|[Aliexpress](http://www.aliexpress.com/item/1pcs-High-Quality-HC-SR501-Infrared-PIR-Motion-Sensor-Module-For-Arduino-Raspberry-pi/32558562655.html) |
|OpenLog|any other way to save or log the bird action is fine, e.g. online services or flash rom|$15|Sparkfun|
|TinyRTC||$0.6|[Aliexpress](http://www.aliexpress.com/item/Free-shipping-20pcs-lot-The-Tiny-RTC-I2C-modules-24C32-memory-DS1307-clock-RTC-module-for/1876368739.html)|
|Atmel 328P|using the bare chip allows us to utilze the full potential of the power saving|$2||
|Solar lamp|a weather proof nice case and solar rechargable battery power supply|$3|[Aliexpress](http://www.aliexpress.com/item/New-Arrival-Solar-Power-Panel-6-LED-Light-Sensor-Waterproof-Outdoor-Fence-Garden-Pathway-Wall-Lamp/32456071230.html)|
|5V voltage boost||$1||
|100nf ceramic capacitor|For smoothing out the power spike during runtime|$0.1||

Expect some soldering, reusing old cables and some connectors.

###Schematics###
Downloadable in this repository. Rough version as I the wiring myself.
![Schematics](https://github.com/barde/bfc3000/raw/master/bfc3000_bb.png)


###Prototype
![Prototype with ATMEGA2560 boad](https://github.com/barde/bfc3000/raw/master/prototype.jpg)

Using an ATMEGA2560 for prototyping has the big improvement of multiple serial ports. One for debugging and other for
the devices, e.g. the OpenLog which communicates over Serial.

It was somewhat fuzzy to get the OpenLog going with my el-cheapo Chinese MicroSD. Firstly, the sensor was blinking
thrice (card error) with its default FAT32 system. I repartitioned to FAT16 and decreased the partition size. It worked
but the card was not removable during a power cycle.

The solution: a firmware update. You need some TTL converter like FTDI to USB or some 
[cheaper
version](http://www.aliexpress.com/item/Free-Shipping-1pcs-FT232RL-FTDI-USB-3-3V-5-5V-to-TTL-Serial-Adapter-Module/32481520135.htm).
Following [this instruction](https://learn.sparkfun.com/tutorials/openlog-hookup-guide) for reprogramming the on board Atmega328 is straight forward.
After flashing it flawlessly wrote to the full sized FAT32 partitioned card.

###Power supply
Due to its size and small expected power consumption it is fit to be powered by a 1.2V NiMh battery. For power
harvesting I reuse a small [solar powered lamp with an included rechargable
battery](http://www.aliexpress.com/item/New-Arrival-Solar-Power-Panel-6-LED-Light-Sensor-Waterproof-Outdoor-Fence-Garden-Pathway-Wall-Lamp/32456071230.html).
Quite nice for $3 as there is lavish space inside for my own sensors and the board. The casing seems
watertight. I put the step up converter in parallel to the battery and used some left over JST connectors.

###Power consumption during runtime
TBD

###Power consumption during sleep
TBD
