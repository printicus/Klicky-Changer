# The X-Endstop

I have searched a solution for using the microswitch on the shuttle as a X-Endstop for a long time. I did not found the software solution, yet(first asterisk). Klipper does not permit multiple endstops per stepper motor.
So I have gone the hardware route for this:
The original cables for my toolboards where to tick and heavy for what I like, so I build myself other cables. I used for this some PTFE Shielded Cable I found on Aliexpress. The cable I bought has 4 wires and is shieldet. I used 2 wire for the usb toolboard, 2 wire for x-endstop, I used the shielding for negative voltage and I runned annother PTFE 18AWG wire for plus voltage. As a bonus, the cable is pretty stiff, and, between the stiffnes of the cable and the PTFE tubing for the filament, I dont need to use anny spring wire or flatband to keep the umbilical nice and straight(second asterisk). On the back of the printer I wired all the umbilical x-endstop wires in paralel and connected them to a empty endstop connector on the motherboard. In front, the umbilical x-endstop wires are connected to two of the pogopins that, when atached to the shuttle, are connected to the x-endstop on the shuttle. In this way I have a working X-endstop on the shuttle that works with all toolheads. I hope I did not make annybody dizzy...

Links:
- PTFE Cable - https://vi.aliexpress.com/item/1005007128144063.html
- XT30(2+2)f Connectors - https://vi.aliexpress.com/item/1005008255764206.html
- Extra plus voltage wire - https://vi.aliexpress.com/item/1005001887468108.html
- Molex Connectors - https://vi.aliexpress.com/item/1005005657577507.html


Now, the asterisks:

- First asterisk:
In fact I did found a software solution that can be used for using the x-endstop pins from each toolboard. This is in an open issue on Viesturz's github (klipper-toolchanger github). https://github.com/viesturz/klipper-toolchanger/issues/35
Its a new version of klippers "multi_pin.py" that, when put in place of the original one, will allow using the multi_pin option to designate multiple pins for an endstop.
It has two issues, how I see it:
1- It will "look" at all pins at once. And because only one toolhead at the time is on the shuttle, that means that at all time it will be, when you have 6 tolheads, one pin triggered and five open. So at al time the endstop is seen as open.
2- It has a big delay between the triggering of the endstop and stoping the motion. Enough to slam the shuttle in the "X-Y joints" printed parts. And I dont know if its from the fact that the multi pin system is not ment for quick reactions, or the new version of multi pin software has some flaws....

- Second asterisk:
I designet my toolboards mounts so that the cable is tilted towards the back of the printer, so it vill better clear the docks when printing under them. For inforcing that tilt I allso use a 30cm 1.5mm music wire. Pictures are in the Images folder.