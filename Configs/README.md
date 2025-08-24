# Configuring Klicky-Changer for Voron 2.4

## Please read all of this first and then start configuring Klicky-Changer.

## KNOWN LIMITATION(AND DANGER):

- Because of how Klicky-Probe software works, the first move when homing after starting the printer, or after the stepper motors disengaging, is by going up by the value of "safe_z", found in the **/Klicky-Probe/klicky-variables.cfg** . This will happen once if you use G28(or "home all" buton on your printer web interface), or it will happen twice if you use G28 XY and G28 Z one after annother. So if it happens that the gantry is stoppend and the stepper motors are disengaged close to your printer max Z hight for some reason( just started the printer, finished print, some errors by docking and undocking, or any other reasons ) do not home the printer or you run the risk of going over your Z hight limit and breack something. Please manualy move the toolhead to the center of your x-y axis and carrefully( after making shure no printed parts are on the printer bed ) use the "UNSAFE_LOWER_GANTRY" macro to lower the gantry to a safer hight. The macro will move the gantry down 20mm. So use it to move the gantry to about the half of your printer Z hight, and then home the printer. Dont use the macro if the toolhead is at bed level, it will crash the toolhead and the shuttle in the bed.

- Homing must be in X-Y-Z sequence. Homing Y-X-Z can lead to colision whit the Klicky-Probe Dock or the magnets from the shuttle can drag the Klicky-Probe down from dock and lead to errors and/or crashes.

- The bed mesh "mesh_min" Y distance should not be smaller than the probe Y offset value ( [tool_probe T(n)] - "y_offset" ). A value of 25 for the "mesh_min" Y will be ok.
- The QGL Y back probe points ("points:") should not be bigger than your Y max bed size minus the probe Y offset value ( [tool_probe T(n)] - "y_offset" ). A value of (your bed Y size minus 40) will be ok.


## Klicky-Changer's functions:

- Its a Toolchanger. You can have as manny toolheads your printer can fit, and use them for multicolor and multimaterial printing.
- It uses Klicky-Probe as a Z-Probe for homing, bed meshing and QGL.
- It uses pin detecton for knowing what tool is mounted.
- If you have the posibility for homing with every toolhead(if you have sensorless setup, or microswitches for x and y) you can home and start a print with whatever toolhead is on the shuttle. No need to make shure T0 is on the shuttle to start printing.


## This is how I have configured my printer.

- This is a configuration for "Z-Probe on all tools and fixet docks", with the tool docks on a aluminium profile placed on the front of the printer(or in a door buffer, if you have one). If you want liftbar you must configure that youself, im not familiar with that.
- This configuration steps are for using Klicky-Changer with my toolhead, MiniBurner XL. Klicky-Changer can be used with other toolheads to(no limitation there), but be carefull. The main difference will be dock configuration. For that you will need to refer to the specific toolhead you want to use.
- First do the Klicky-Changer configuration as it is. If you decide to do changes in files and/or configs other than what is mentioned in this guide, you may get errors... I run my printer with this configs for a long time now and i got no errors or crashes.
- Homing is handled by Klicky-Probe homing_overide macro. You can find it in **/Klicky-Probe/klicky-macros.cfg**. As it is now, its set for homing with regular microswitches for X and Y. If you want to use sensorless homing you will need to ad macros for that. The macros must be named "_HOME_X" for sensorless X, and "_HOME_Y" for sensorless Y. Allso you must do the rest of the sensorless homing configuration in your printer.cfg.
- After every file modification do a "firmware restart". Until the configuration is finished allways home with T0.

First, please, do a back-up of your configs.
Have the hardware part sorted out(wireing, shuttle, backplates with toolheads, toolheads docks, klicky-probe dock...)

The printer must have klipper and all configs instaled, and functioning as a printer(for best results I recomand a fresh klipper install). For that refer to your Mainboard documentation and your printer manual. If you already have Klicky-Probe(or PCB-Klicky) hardware installed(the probe dock) it will make this setup easier. Delete all klicky-probe files and configs from your printer config folder, Klicky-Changer comes with its own configs for Klicky-Probe. Allso no Kamp or other pluggins for whatever function you have installed. Those can be addet after Klicky-Changer is fully functional, if you still need them.

SSH into your printer(refer to your Mainboard docs for how to do this) and run the installation script for the Klipper-Toolchanger plugin using the following command:
```
wget -O - https://raw.githubusercontent.com/printicus/klipper-toolchanger/main/install.sh | bash
```
This script will download the Klipper-Toolchanger plugin to your RaspberryPi home directory, and symlink the files in the Klipper extra folder.

- Copy "Klicky-Probe", "Klipper-Toolchanger" and "Toolheads" folders from this repo to your printer config folder.
- Copy "My_MACROS.cfg" and "prime_lines.cfg" to your printer config folder.
- Ad the lines from this "printer.cfg" to your "printer.cfg". Use these macros to replace your printer.cfg macros.
- Delete, or comment out, the [probe] section from your printer.cfg file. Each toolhead config file will have its own probe section.
- Reboot your printer

You will need to change the pins in each toolhead configs for the pins of the toolboard atached to it, and ad toolheads configs for all your toolheads. I only posted two as an example.

You will need to set Klicky-Probe dock position: https://github.com/jlas1/Klicky-Probe/tree/main/Printers/Voron/v1.8_v2.4_Legacy_Trident#step-6-klipper--dockundock-configuration

## Setting T0 Probe Z-Offset(the paper sheet method):

- You will need to ad in each tool config the probe Y offset ( [tool_probe T(n)] - "y_offset" ). The value for both shuttles(for Klicky-Probe and PCB-Klicky) is 22.45.

- G28 - QGL - G28(or use the G32 macro includet, it does the same thing, but with fewer probe docking and undocking)
- Make shure the probe is not atachet to the toolhead.
- Move the toolhead to the middle of the bed, imput "G0 Z0" into the console.
- Put a paper sheet on the bed, under the nozzle. Use the Z-Offset controls in your web interface to bring the nozzle down untill it lightly touches the paper. Adjust the z-offset until you feel a small amount of friction when pushing the paper back and forth. The resulted Z-Offset will be a negative number( for example: -4.2 ). You will put that number in your T0 config under "[tool_probe T0]" - "z_offset:", but as a positive number( for example: 4.2).
- Do a one layer print test for fine tunning the first layer z-offset, and adjust the T0 z-offset value in your T0 config file accordingly.

The formula for finding the new value for Z-offset is: the z-offset from the T0 config-(the new z-offset).
For example: the z-offset from the T0 config is 4.2 and the new z offset after adjusting for better first layer is, lets say, -0.12(how it shows in the web interface z-offset). That results in 4.2-(-0.12), and after math rules its 4.2+0.12=4.32 Thats the new value for T0 z-offset.

Value adjusting in the toolheads configs must be done manually, not with the "save config" command.

After you have a first layer to be proud of, write that Z offset value in all your tools configs([tool_probe T(n)] - "z_offset:")
If you will need to again fine tune the T0 z-offset and it will be a different value(usually a very small difference do to the plastic on the touching points between shuttle and backplate settling after repeated toolchanges) you will need to write the new Z-offset value in all tools configs.

## Setting dock position

## Definition: "docked position" is the toolhead position fully seated on the dock, waiting to be picked-up.

After setting T0 Z-offset, and with T0 on the shuttle:
1. G28 - QGL - G28(or use the G32 macro includet, it does the same thing, but with fewer probe docking and undocking)
2. Using the web interface move your toolhead to his designated dock so that it will be in the "docked position", as precise as you can. Write the X and Y coordonates shown in the Toolhead position on your web interface in your T(n)(n = what number toolhead you have on the shuttle) config, under [tool T(n)] section's "params_park...". For Z coordonates you will need to ad 1mm and do the same. 
3. Carefully backup the toolhead from the dock , and lower the gantry to about 50-100 Z position. Do a "Firmware Restart".
4. After restart, with T0 on the shuttle, do a G32. Manually swap T0 with next toolhead that needs dock setting. Go to step 2. If all toolhead have the dock positiom set, go to step 5.

Usually, when all toolheads and docks are the same model, the Y and Z "docked position" for all toolhead should be the same. But dont rely on this...

5. For testing and safety purposes, change the "params_fast_speed" and "params_path_speed" in the /Klipper-Toolchanger/toolchanger.cfg file to a much lover value. Lets say 5000 and 300. Do a "Firmware Restart". After the testing is done you will revert this change.
6. With T0 on the suttle do a G32. When finished, atempt a toolchange by using the Tools macro. Be ready to catch the toolhead if something goes wrong... Adjust the dock position coordonates if needet untill the toolchanges are done whitout problems.

## Setting the other toolheads(T1, T2, etc) g-code z-offset(not T0)

1. With T0 on the shuttle do a G32. Use the tools macro to do a toolchange for the next tool that needs setting the g-code z-offset. Move the tool to the middle of the bed, input on the console G0 Z1. See if the nozzle is touching the bed. If not, use the web interface to move to toolhead down to Z0 in small steps(0.1mm). 
2. If you got to Z0 and the nozzle is not touching the bed, put a piece of paper under the nozzle and use the z-offset controls to lower the nozzle until it touches the paper. Adjust that until you feel a small amount of friction when pushing the paper back and forth. Go to step 4.
3. If the nozzle is touching the bed before you got to Z0, rise the nozzle with the z-offset controls by 0.1 mm, then lover the nozzle with the tool position controls by 0.1mm. Do this until the toolhead is at Z0 and the nozzle does not touch the bed. Go to step 2.
4. The value shown in the web interface under z-offset is the value you must write in your T(n) tool config in [tool T(n)] section under "gcode_z_offset:" This time the value must be writen as shown in the web interface. Do a "Firmware Restart".
5. If all other toolheads have the g-code z-offset set, next step is X and Y gcode offsets. If not, go to step 1.

You must, as with T0, do a one layer print test with each toolhead to fine tune that first layer. The new value shown in the web interface z-offset position must replace the value in that toolhead gcode z-offset setting.
The gcode z-offset value adjusting in the toolheads configs must be done manually, not with the "save config" command.


## Setting the toolheads(T1, T2, etc) g-code X and Y offsets.

The X and Y gcode offsets are needet so that all nozzles after T0(T1, T2, etc) are alignet with T0 nozzle.

Guides on how to do that can be found in the links bellow. 

I use a nozzle camera and "axiscope" to do that. https://github.com/nic335/Axiscope

But there are allot of other methods:

By printing: https://www.printables.com/model/201707-x-y-and-z-calibration-tool-for-idex-dual-extruder

NozzleAllign - https://github.com/viesturz/NozzleAlign

Nudge - https://github.com/zruncho3d/nudge

kTAMV - https://github.com/TypQxQ/kTAMV


In theory, thats it. Your setup my need some adjustments over time, but its ready to print. Good Luck.