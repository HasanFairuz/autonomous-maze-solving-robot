# Hardware and software design

[Back to README](../README.md)

## Hardware observed and configured

The archived ROBOTC configuration maps two touch sensors to `S1` (right) and `S4` (left), an ultrasonic sensor to `S2`, and EV3 large drive motors to `motorA` (right) and `motorD` (left). The photographs show the EV3 brick, a paired forward-facing sensor assembly, two large wheels, and a compact chassis.

## Motion control

`turnRight()` and `turnLeft()` command opposite wheel velocities until an encoder threshold of 580 is reached. `goFwd()` commands both motors forward until the left encoder reaches 1450 counts. These are code constants, **not independently measured motion accuracy**. `bumpAdjust()` drives against a wall until both bumpers activate, then backs away to improve alignment. This wall-contact calibration depends on the robot and maze geometry.

## Maze model

`maze[4][6]` holds a `cell` with north/east/south/west wall fields. The current robot heading, row, and column are kept in global variables. The implementation sets perimeter boundaries, updates observed blocked walls and neighboring cell wall fields, and displays the current wall map on the EV3 LCD using `drawLine()`.

## Display and feedback

`robDraw()` erases the display, draws wall lines and places a heading glyph in the current cell. On reaching the target, the code shows `SOLVED !`; on completing the reverse route, it alternates `RETURNED !` with the maze display. An obstacle detection event also triggers a sound.

## Important scope note

The supplied source is a ROBOTC/EV3 program. MATLAB is not necessary for this archived implementation and no MATLAB script was provided.
