---
title: Calibration
layout: home
---

```
G28 X Y
G28 X150 Y150
CARTOGRAPHER_CALIBRATE METHOD=MANUAL
SAVE_CONFIG
G28 X Y
G28 X150 Y150
CARTOGRAPHER_THRESHOLD_SCAN MIN=400 MAX=3500
SAVE_CONFIG
```

add SURVEY_HOME to Print Start Macros/Procedure found in [Macros](macros.html)
By default Z_offset:1.0 is too high, in the next steps we will adjust this.

Begin a Print
Babystep Z down to perfect height
```
save_tap_offset
save_config
```
