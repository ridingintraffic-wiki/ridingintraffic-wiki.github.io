---
title: "bl touch printer gcode"
date: 2023-03-04
---
## Marlin gcode ender3
If you wanted to run bltouch and do a bed level mesh every print  this is one way that you could do it.  

```
; Ender 3 Custom Start G-code
M117 Getting the bed up to temp!
M140 S{material_bed_temperature_layer_0} ; Set Heat Bed temperature
M190 S{material_bed_temperature_layer_0} ; Wait for Heat Bed temperature
M117 Pre-heating the extruder!
M104 S160; start warming extruder to 160
G28 ; Home all axes
M117 Auto bed-level GO!
G29 ; Auto bed-level (BL-Touch)
M500;
G92 E0 ; Reset Extruder
M117 Getting the extruder up to temp!
M104 S{material_print_temperature_layer_0} ; Set Extruder temperature
M109 S{material_print_temperature_layer_0} ; Wait for Extruder temperature
G1 Z1.0 F3000 ; move z up little to prevent scratching of surface
G1 X0.1 Y20 Z0.3 F5000.0 ; move to start-line position
M117 LET THE PURGE BEGIN!
G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; draw 1st line
G1 X0.4 Y200.0 Z0.3 F5000.0 ; move to side a little
G1 X0.4 Y20 Z0.3 F1500.0 E30 ; draw 2nd line
G92 E0 ; reset extruder
G1 Z1.0 F3000 ; move z up little to prevent scratching of surface
M420 S1;
M117 Autobots! Roll Out!
; End of custom start GCode
```