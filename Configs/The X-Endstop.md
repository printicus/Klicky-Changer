# The X-Endstop

I have searched a solution for using the microswitch on the shuttle as a X-Endstop for a long time. I did not found the software solution, yet. Klipper does not permit multiple endstops per stepper motor.
So I have gone the hardware route for this:

The original cables for my toolboards where to tick and heavy for what I like, so I build myself other cables. I used for this some PTFE Shielded Cable I found on Aliexpress. The cable I bought has 4 wires and is shieldet. I used 2 wire for the usb toolboard, 2 wire for x-endstop, I used the shielding for negative voltage and I runned annother PTFE 18AWG wire for plus voltage. As a bonus, the cable is pretty stiff, and, between the stiffnes of the cable and the PTFE tubing for the filament, I dont need to use anny spring wire or flatband to keep the umbilical nice and straight(first asterisk). On the back of the printer I wired all the umbilical x-endstop wires in paralel and connected them to a empty endstop connector on the motherboard. In front, the umbilical x-endstop wires are connected to two of the pogopins that, when atached to the shuttle, are connected to the x-endstop on the shuttle. In this way I have a working X-endstop on the shuttle that works with all toolheads. I hope I did not make annybody dizzy...

Links:
- PTFE Cable - https://vi.aliexpress.com/item/1005007128144063.html
- XT30(2+2)f Connectors - https://vi.aliexpress.com/item/1005008255764206.html
- Extra plus voltage wire - https://vi.aliexpress.com/item/1005001887468108.html
- Molex Connectors - https://vi.aliexpress.com/item/1005005657577507.html


Now, the asterisk:

- First asterisk:

I designet my toolboards mounts so that the cable is tilted towards the back of the printer, so it vill better clear the docks when printing under them. For inforcing that tilt I allso use a 30cm 1.5mm music wire. Pictures are in the Images folder.
