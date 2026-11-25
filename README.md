# SV06-Plus-y-motor-upgrade/replacement-17HS5415P1-X6
An upgrade/replacement guide for the Sovol SV06 Plus 3D Printer Y Axis motor to get up to ~9000mm/s^2 Acceleration at 650 mm/s on the y axis. My Stock Y Motor broke and a replacement would cost more than 25€. So I decided to buy a motor for 10€ with way better specs: The 17HS5415P1-X6. The issue is the port. So here is a way to make it usable.



Safety note: This guide documents the modification I tested on my own Sovol SV06 Plus. Incorrect wiring or exposed solder joints can cause a short circuit and damage the printer. Switch off and unplug the printer before connecting or disconnecting either motor. Insulate every solder joint and verify the wiring with a multimeter before powering the printer on. The Klipper settings shown are the values I used on my printer.


## What you need
- Klipper on your printer (!)
- The 17HS5415P1-X6 1.5A Stepper motor
- Soldering Iron and Solder
- Heat-shrink tubing
- Stepper motor Port (JST-PH) I salvaged mine from the old, broken motor
- Screwdriver
- tools to cut the cables and strip the insulation
- Glue / Double-sided tape

<p align="center">
<img width="420"  alt="" src="https://github.com/user-attachments/assets/28090c51-ea9d-48bd-822a-f99b125e7b85" />
</p>

## Step one: Preparing the port
<p align="center">
<img width="420"  alt="" src="https://github.com/user-attachments/assets/39ba3ed9-2f91-4b2f-bfb3-7695c2a64454" />
</p>
Bend the needed Pins of the JST-PH Port to the other side (Around 130°). This allows an easy installation and attachment to the motor later. For the SV06 Plus Motherboard, you only need the two inner pins and the two outer pins, but you have to bend the other pins as well so that they do not get in the way of the casing (I bent the unneeded one a little less).




## Step two: Connecting port with wires
<p align="center">
<img width="420"  alt="" src="https://github.com/user-attachments/assets/f4649291-aa29-4a62-a476-a29c45cec682" />
</p>

Start by cutting the 4 wires of the motor and stripping the insulation so that you get a blank Cable about the length of 3/4 of the pins on the JST-PH Port. 
Pretin the wires and port pins. 
Now you need to find out where the phases of the new motor are. I used a multimeter to check for resistances. For me, the blue and red wires belonged to one coil, black and green to the other. 
For the Sv06 plus motherboard, the correct phases on the connector are marked on the image.

Slide a piece of heat-shrink tubing onto each of the wires and slide them back so that they do not get warm as you solder. Solder the wires to the pins.
**Optional:** You can test if you did it right by connecting the cable of the old y motor to the new one. After that, unplug it again and continue.
After that, use the heat-shrink tubing to cover up the soldered connections


## Step three: Preparing the motor
<p align="center">
<img width="420"  alt="" src="https://github.com/user-attachments/assets/b887b278-26fe-4753-8240-140e7cdb6e91" />
</p>

Place a piece of double-sided tape on **The same side/spot as on the image**. This will keep the wires from sticking up and potentially rubbing against the bed. You can also add glue to make the connection stronger. But pay attention to the heat rating of the materials you use.


## Step four: Installation 
- Unplug the printer completely
- Unscrew the belt tension mechanism completely
- Remove the belt from the pulley and unplug & unscrew the motor
- Take off the pulley from the shaft of the old motor by loosening the screws. For me, this required some force as there was some kind of glue used.
- Place the pulley on the shaft of the new motor and secure it by tightening the screws. 
- Screw the new motor onto the mount with **the cables coming out of the motor at the bottom**
- Place the belt on the pulley and tighten it
- Connect the wire and start the printer

## Step five: Config
<p align="center">
<img width="420"  alt="" src="https://github.com/user-attachments/assets/1dcfd01c-d0ab-4292-b461-4907351f2ad6" />
</p>

These are my config settings. If you noticed that your bed moves in the wrong direction (which it did for me), place an ! before the PB7 at dir_pin. You could also switch a pair of wires (same phase) on the connector, but this seemed unnecessary for me. 
I increased the run current to 1A. The motor is rated for 1.5A, but I did not want to overload the driver. You also may have to change the sensitivity of the homing detection by changing driver_SGTHRS. A higher number means a more sensitive detection. Mine worked fine at 100.




## Results
After a few tests, the max Acceleration I could reach was 9k mm/s^2 at a speed of 650mm/s (I unplugged the X Motor for this test). However, this was the absolute max for me. Anything after that, the y motor started to skip steps. 
For everyday use, I settled for 6500 mm/s^2 at 750 mm/s. I also ran a speed test at 7000 mm/s^2 and 800 mm/s with 20 iterations for all motors and it completed all 20 iterations without any skipped steps.


