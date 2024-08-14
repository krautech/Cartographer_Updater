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

[gcode_macro SURVEY_HOME]
rename_existing: _SURVEY_HOME
gcode:
    {% set SURVEY_TEMP = printer.configfile.survey_temp|default("150")|int %}
    {% set MAX_TEMP = SURVEY_TEMP + 5 %}
    {% set ACTUAL_TEMP = printer.extruder.temperature %}
    {% set TARGET_TEMP = printer.extruder.target %}
    {% if not "xyz" in printer.toolhead.homed_axes %}
        { action_respond_info("Printer not homed")}
    {% else %}
        {% if TARGET_TEMP > SURVEY_TEMP %}
            { action_respond_info('Extruder temperature target of %.1fC is too high, lowering to %.1fC' % (TARGET_TEMP, SURVEY_TEMP)) }
             M109 S{ SURVEY_TEMP }
        {% else %}
            # Temperature target is already low enough, but nozzle may still be too hot.
            {% if ACTUAL_TEMP > MAX_TEMP %}
                { action_respond_info('Extruder temperature %.1fC is still too high, waiting until below %.1fC' % (ACTUAL_TEMP, MAX_TEMP)) }
                TEMPERATURE_WAIT SENSOR=extruder MAXIMUM={ MAX_TEMP }
            {% endif %}
        {% endif %}
        {% set home_x, home_y = printer.configfile.config.scanner.tap_location.split(',')|map('trim')|map('float') %}
        G90
        G0 X{home_x} Y{home_y} F10000
        M400
        _SURVEY_HOME
        M109 S{ TARGET_TEMP }
    {% endif %}
```
