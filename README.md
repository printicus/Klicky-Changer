# Klicky-Changer 

Dont go past Klipper v0.13.0-669. For this use the folowing:

```
sudo service klipper stop
cd ~/klipper
git checkout fb57d59ce0aeebfe63d0f7c5d716ee9119faf029
sudo service klipper start
```
After that, if you have a klipper warning, do a "soft reset" not "hard reset", or you will need to reinstall all other addons.


### (fully functional, thing are still being added, modified...)
 
Short demo print featuring [Miniburner XL Toolhead](https://github.com/printicus/For-Voron-Printers/tree/main/MiniBurner_XL_Toolhead).

[![Test Print](https://img.youtube.com/vi/o_eyPX9v53s/0.jpg)](https://www.youtube.com/watch?v=o_eyPX9v53s)

50 toolchanges demo

[![Test Print](https://img.youtube.com/vi/J430dFG2X50/0.jpg)](https://youtu.be/J430dFG2X50)

[DISCORD INVITE](https://discord.gg/PGrTdSWV) or [DISCORD CHANNEL](https://discord.com/channels/1119433664799965186/1412843406224523347)

Klicky-Changer is a toolchanger hardware addon for Voron 2.4 and other similar setups, what uses Klicky Probe(or PCB Klicky) as Z probe. Its inspired from the three pin shuttle and backplate interlocking design from [DraftShift Design](https://github.com/DraftShift/StealthChanger) and uses Viesturz's [klipper-toolchanger](https://github.com/viesturz/klipper-toolchanger) software and modified [Klicky-Probe]( https://github.com/jlas1/Klicky-Probe ) configs.

Thanks to the above mentioned sources for my inspiration, without their work my days would be much empty.

This is a ME project. I designet, remixed or modded these files for me, but I uploaded them here, maybe someone will find them interesting and will want to use them. I use Super Slicer as my slicer of choice, wich has an option for "Vertical Hole shrinking compensation" that allows me to tune vertical holes diameter without modifying other dimensions. This will make the vertical holes a bit smaller when my files are used with other slicers, especially for screw holes ment for selftapping. Be aware of that, or parts will break!

I included a file for vertical hole tuning if you want to do that.
