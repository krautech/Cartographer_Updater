---
title: Macros
layout: home
---
```
[scanner] # update cartographer to scanner
canbus_uuid:51eb6e4f876d # EDIT THIS TO SUIT YOURS
#serial: /dev/serial/by-id/usb-Cartographer_614e_110001800643564738333920-if00
speed: 2.0
lift_speed: 5.0
backlash_comp: 0.02
x_offset: 0.
y_offset: 21.1
trigger_distance: 2.0
trigger_dive_threshold: 1.5
trigger_hysteresis: 0.006
cal_nozzle_z: 0.1
cal_floor: 0.1
cal_ceil:5.
cal_speed: 1.0
cal_move_speed: 10.
default_model_name: default
mesh_main_direction: x
mesh_cluster_size: 1
mesh_runs: 2
detect_threshold_z: 400 # This needs tuning
calibration_method: tap
z_offset: 0.00
sensor: cartographer
probe_speed: 2.0
tap_location: 175,175 # set to center of bed
survey_temp: 150
```
