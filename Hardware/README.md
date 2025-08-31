# Klicky-Changer hardware parts

[![Klicky Changer](https://img.youtube.com/vi/5xcj8SzUP70/0.jpg)](https://www.youtube.com/watch?v=5xcj8SzUP70)

## Here you can find the designs for the Klicky-Changer hardware parts.

There is a shuttle for using with classic Klicky-Probe and a shuttle for using with PCB Klicky.
The PCB (from the PCK Klicky kit)that has the JST connector must be modified. Because of space constraints the connector must pe removed(just the plastic part), the pins shortened and the wires that come from the pogopins will be soldered direct on the pins(see picture)

<img src="../Hardware/Images/Shuttle PCB Klicky 05.jpg" width="350" >

After some testing I decidet to go with magnets ment to be screwed on, rather than forced into the printed parts. Printed parts tend to loosen over time and the magnets are puled out after repeated use. Glue does not do much.

I gave the option to use double the magnets between the shuttle and backplate. You can choose if you use two pairs or four pairs, depending on what strengt magnets you have. In a normal case, just two magnets on the shuttle, one on each side, and two magnets on the backplate is enough.

The electrical connection between shuttle and backplate is done with pogopins. This is for wireing the Z-probe connection, x-endstop(if you will use it) and for pin detection.


## Pin Detection

For that I use 4 of the 8 pogopins contacts. On the shuttle side solder 4 pogopins together. On the backplate side the corespondent pogopins are soldered 2 and 2. I do this so I will double the contacts uset for tool detection. I dont want after 10 hours printing to get a bad contact and scrap the print. Because I dont use filament detection, the pins for that I use for tool detection. You can use whatever free pins you have on your toolboard.

<img src="../Hardware/Images/Pogopins Wireing Example - Shuttle.jpg" width="350" >  <img src="../Hardware/Images/Pogopins Wireing Example - Backplate.jpg" width="350" >

## Bom for one shuttle:

- Filament: ABS or ASA
- Endstop switch D2F-L x2 (when used for x endstop the lever stays on, when used for Klicky-Probe the lever must be removed)
- Magnets: 6x3x2mm magnets  x7. This does not include the magnets on the probe itself.
- M2x10  x7 Countersunk Self Tapping Screws for magnets
- Pogopins with 8 contacts. They are sold in pairs. On the shuttle will be used the non springy ones.
- M1.5x4  x2 Self Tapping Screws for the pogopins.
- Thin wires. I've measured them as 0.6mm.
- 4x6x6 Bushings  x3 (Cheap items, buy more than you need and try them out until you find a set that works the best....)

## Bom for probes: BOM can be found on theyr respective Github.

From Klicky Probe github you will need to print the probe and the probe dock(the probe dock will be used allso for PCB-Klicky)
From the PCB-Klicky github you will need to print the probe.

## Links:

- Magnets:  https://www.buyneomagnets.com/p/6mm-dia-x-3mm-thick-with-countersunk-hole-2mm-n35-strong-countersunk-neodymium-disc-magnets-countersunk-ring-rare-earth-magnet

- Endstop switch: https://vi.aliexpress.com/item/1005005222652017.html

- Bushings: https://vi.aliexpress.com/item/1005005335880614.html

    or https://vi.aliexpress.com/item/1005007954250796.html
  
    or https://vi.aliexpress.com/item/1005005924778460.html

- Pogopins I used:  https://vi.aliexpress.com/item/1005006125313623.html  the model I used is "8P with ear 2.54mm". Buy 1-2 pairs extra, maybe, over time the backplate side ones may get bad... not happened to me yet, but nothing is perfect.

- Screws for pogopins: https://vi.aliexpress.com/item/1005003934120055.html

- Screws for magnets - https://vi.aliexpress.com/item/1005006676743568.html

- PCB Klicky kit: https://vi.aliexpress.com/item/1005005467101449.html
- PCB Klicky Github for printed parts: https://github.com/tanaes/whopping_Voron_mods/tree/main/pcb_klicky

- Klicky-Probe Github for printed parts and guides: https://github.com/jlas1/Klicky-Probe

## Recomendet tools

One set of allen keys, Philips small screw-drivers, box cutter, Drill bits starting at 1mm, Side Cutters, pliers, ruler, calipers, etc

Drill Bits Sets: https://vi.aliexpress.com/item/1005004411348630.html
You will need to make shure the holes for the M1.5 and M2 selftapping screws are the rigt size, or parts will break. For the M1.5 screw I use the 1mm drill bit to redrill the hole and for the M2 I use the 1.5mm drill bit.

## Printing

I use primarely SuperSlicer. My designs are made to take advantage of the "Vertical Hole shrinking compensation" setting in that slicer, that lets me tune vertical hole size without altering other dimensions. So if you will slice my files with other slicers, the vertical holes will come out smaller. The holes ment for self tapping screws are the most problematic in this situation. Maybe you will need to redrill them to fit screws trough. I includet a file for tuning the hole size, if you want to use it.


4 walls, 5 tops, 5 bottoms. 40-50% infill. Only pink color allowed.... :D





