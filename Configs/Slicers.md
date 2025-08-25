# This is how I have configured my slicers

## I use SuperSlicer and Prusa Slicer. My instructions are for these two slicers.

I will, eventually, get the instructions on how to use with Orca Slicer allso

My primary Print_Start is in the slicer.

## - For Super Slicer:

In the Printer Setting tab, under Custom G-code:
 - In the "StartG-code" window I have:

```
BED_MESH_CLEAR
G28 x y
Attach_Probe_Lock
G28 z
G90
G0 X30 Y30 Z100 F20000              ; move nozzle away from bed
M190 S[first_layer_bed_temperature] ; wait for bed temp to stabilize
QUAD_GANTRY_LEVEL
G28
BED_MESH_CLEAR
BED_MESH_CALIBRATE ADAPTIVE=1
Dock_Probe_Unlock
G0 X30 Y30 Z100 F20000              ; move nozzle away from bed
PRINT_START TOOL_TEMP={first_layer_temperature[initial_tool]} {if is_extruder_used[0]}T0_TEMP={first_layer_temperature[0]}{endif} {if is_extruder_used[1]}T1_TEMP={first_layer_temperature[1]}{endif} {if is_extruder_used[2]}T2_TEMP={first_layer_temperature[2]}{endif} {if is_extruder_used[3]}T3_TEMP={first_layer_temperature[3]}{endif} {if is_extruder_used[4]}T4_TEMP={first_layer_temperature[4]}{endif} {if is_extruder_used[5]}T5_TEMP={first_layer_temperature[5]}{endif}  BED_TEMP=[first_layer_bed_temperature] TOOL=[initial_tool]
```

 - In the "Tool change G-code" window I have:

```
{if layer_num > 0}
M104 S{temperature[next_extruder]} T[next_extruder] ; set new tool temperature so it can start heating while changing
{else}
M104 S{first_layer_temperature[next_extruder]} T[next_extruder] ; set new tool temperature so it can start heating while changing
{endif}
M106 S0
T[next_extruder]
{if layer_num > disable_fan_first_layers -1}
M106 S{default_fan_speed *2.55}
{endif}
```

This will start preheating your next tool acording to what layer it will be printing. If you have in your slicer different temps for first layer and the other layers it will preheat accordingly. It will also stop the PCF for the toolchange, so it will not interfere with the temp stabilization, and will start the PCF only at the layer that you have it set in the Filament Settings tab, under Cooling, and at the speed you have it set.


## - For Prusa Slicer:

In the Printer Setting tab, under Custom G-code:
 - In the "StartG-code" window I have:

```
BED_MESH_CLEAR
G28 x y
Attach_Probe_Lock
G28 z
G90
G0 X30 Y30 Z100 F20000            ; move nozzle away from bed
M190 S[first_layer_bed_temperature] ; wait for bed temp to stabilize
QUAD_GANTRY_LEVEL
G28
BED_MESH_CLEAR
BED_MESH_CALIBRATE ADAPTIVE=1
Dock_Probe_Unlock
G0 X30 Y30 Z100 F20000         ; move nozzle away from bed
PRINT_START TOOL_TEMP={first_layer_temperature[initial_tool]} {if is_extruder_used[0]}T0_TEMP={first_layer_temperature[0]}{endif} {if is_extruder_used[1]}T1_TEMP={first_layer_temperature[1]}{endif} {if is_extruder_used[2]}T2_TEMP={first_layer_temperature[2]}{endif} {if is_extruder_used[3]}T3_TEMP={first_layer_temperature[3]}{endif} {if is_extruder_used[4]}T4_TEMP={first_layer_temperature[4]}{endif} {if is_extruder_used[5]}T5_TEMP={first_layer_temperature[5]}{endif}  BED_TEMP=[first_layer_bed_temperature] TOOL=[initial_tool]
```

 - In the "Tool change G-code" window I have:

```
{if layer_num > 0}
M104 S{temperature[next_extruder]} T[next_extruder] ; set new tool temperature so it can start heating while changing
{else}
M104 S{first_layer_temperature[next_extruder]} T[next_extruder] ; set new tool temperature so it can start heating while changing
{endif}
M106 S0
T[next_extruder]
{if layer_num > disable_fan_first_layers[current_extruder] -1}
M106 S{min_fan_speed[current_extruder] *2.55}
{endif}
```


This will start preheating your next tool acording to what layer it will be printing. If you have in your slicer different temps for first layer and the other layers it will preheat accordingly. It will also stop the PCF for the toolchange, so it will not interfere with the temp stabilization, and will start the PCF only at the layer that you have it set in the Filament Settings tab, under Cooling, and at the speed you have it set.

