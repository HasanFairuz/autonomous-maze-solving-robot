# Navigation, return path, and limitations

[Back to README](../README.md)

## Project goal vs. implementation

The MSE 110 competition brief requested autonomous exploration of an unknown 4 × 6 maze and return via the shortest route, with a graphical maze display. The published source implements right-wall-following exploration and reverse traversal of a **simplified recorded path**, rather than an optimal path search across all explored cells. The distinction matters: cancellation of immediate reversals can remove dead-end detours but is not equivalent to breadth-first search or another global shortest-path planner.

## Exploration

The code rotates right first, checks for an obstacle using ultrasonic range (`< 12` in the sensor's API units), realigns using touch sensors if blocked, and otherwise advances a cell. It records the heading for each forward step until the robot coordinates equal the target coordinates. Maze walls are stored in per-cell directional flags.

## Return

A fixed-size stack reduces adjacent movements that are opposites, reverses the remaining heading sequence and navigates it in reverse. This is intended to remove some unnecessary movements made during exploration.

## Known constraints and engineering lessons

- The maze representation is fixed at **4 × 6** cells; this version is not generalized to arbitrary maze dimensions.
- The original team README says the robot **does not handle mazes with islands**.
- Position and heading are estimated using commanded motion and encoder counts; there is **no absolute localization**. Mechanical drift motivated bumper-based realignment.
- The return routine is **not guaranteed globally shortest**, and does not minimize the number of turns.
- Hard-coded thresholds (including turn and step encoder counts) require calibration for the actual robot, wheels, gearing and maze dimensions.
- Path and stack arrays have fixed capacity (100). No overflow handling is implemented for longer routes.
- The team reported resolving robot-orientation difficulties and working to reduce its footprint; time management was identified as a lesson learned.
- No video, benchmark timings, success-rate measurements, or reproducible test fixtures are included in this archive.

## Verification status

The implementation and photos were supplied from the original project archive. This public copy has been privacy-sanitized but **not independently compiled, simulated, or tested on EV3 hardware**. Statements about demonstrated performance are attributed to the original team's notes rather than independently validated.
