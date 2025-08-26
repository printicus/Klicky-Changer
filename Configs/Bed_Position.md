The printer bed position should be as in front of the printer as possible. It makes it easy to ad accessorie in the back of the printer bed(nozzle scrubbers, klicky-probe dock, nozzle probes, etc).


For this you will home your printer, then move your toolhead to Y0. Make a mark on the XY joints printed parts and on the correspondent gantry extrusion, disengage the stepper motors, manualy move the gantry forward untill it touches the front idlers and measure the distance between the mark on the XY joints printed parts and the mark on the gantry extrusion.

<img src="../Hardware/Images/Bed Position 01.jpg" width="500">  <img src="../Hardware/Images/Bed Position 02.jpg" width="500">

That distance measured minus 1mm(you dont want the gantry to slam in the front idlers when going Y0) must be added to the value found in printer.cfg in your Y motor config as "position_endstop:" and "position_max:". Al other accessories you allready have configured and depend on Y position must have the Y position corected in their config.

After an "firmware_restart" home the printer, move the toolhead to Y0 and move the bed so that the edge of the bed to coincide with the tip off the nozzle.

