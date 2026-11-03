<div align="center">

# Autonomous Maze-Solving Robot — LEGO Mindstorms EV3

**ROBOTC · Ultrasonic sensing · Touch sensors · Motor encoders · Maze mapping · Route simplification**

A group-built autonomous mobile robot developed for **MSE 110: Mechatronic Design I** at **Simon Fraser University**. The LEGO Mindstorms EV3 robot was designed to navigate a **4 × 6 cell maze**, sense walls, maintain an in-memory maze representation, and return towards its starting position after reaching a configured target.

</div>

---

## Project at a glance

| Item | Details |
|---|---|
| Platform | LEGO Mindstorms EV3 |
| Programming | ROBOTC (EV3-specific API) |
| Navigation | Right-wall-following exploration |
| Sensors | EV3 ultrasonic sensor, two touch sensors, motor encoders |
| Maze representation | 4 × 6 array of cells, four wall states per cell |
| Return navigation | Recorded route simplification and reverse traversal |
| Display | EV3 screen draws mapped walls and direction indicator |
| Academic context | MSE 110, Group 17, SFU |

## System overview

The robot uses two independently driven EV3 large motors for motion. An ultrasonic sensor detects obstacles ahead, while two mechanical touch sensors help with wall-contact realignment. Encoder thresholds control approximately one-cell moves and 90-degree turns. The program tracks the current row, column and heading as it travels, and redraws its mapped walls and position on the EV3 screen.

### Navigation and return logic

1. Start after a touch-sensor press and initialize the 4 × 6 maze's outer boundary walls.
2. Follow a right-hand-rule exploration strategy; probe forward with the ultrasonic sensor and update wall flags when a wall is detected.
3. Use motor encoders for turns and movement, with touch-sensor-assisted alignment at walls.
4. Record movement headings until the configured target coordinates are reached.
5. Simplify the recorded route by cancelling consecutive opposite-direction movements, then traverse its reverse to return.

**Algorithmic qualification:** This implementation simplifies the route actually travelled. It does **not** perform a full-graph shortest-path search, and no claim of a globally shortest route is made.

## Demonstration

![EV3 maze-solving robot demonstration](media/Maze%20Solving.gif)

*Animated demonstration of the EV3 robot navigating the maze.*
## Robot photographs

### Prototype on the workbench

<p align="center">
  <img src="media/Maze%20Solver.jpg" alt="EV3 maze-solving robot on the workbench" width="520" />
</p>

### Robot in the test maze

<p align="center">
  <img src="media/Maze%20Solver%20In%20Action.jpg" alt="LEGO EV3 robot navigating the physical test maze" width="520" />
</p>

## Source and technical notes

- [ROBOTC implementation](src/MazeSolverPhysical.c) — original program logic, with student identification numbers removed.
- [Hardware and software design](docs/SYSTEM_DESIGN.md) — control architecture, sensors, movement, and maze model.
- [Navigation algorithm and limitations](docs/NAVIGATION_AND_LIMITATIONS.md) — method, assumptions, known limitations, and the distinction between route simplification and shortest-path optimization.

## Outcomes and limitations

The group's original project README reports maze-solving and return-navigation capability in the intended 4 × 6, no-islands environment. The provided photographs establish the physical EV3 prototype. The original submission does not include quantitative success rates, timed trials, an independent demonstration video, or an externally verified test log; those claims are therefore omitted here.

Noted limitations include constrained maze dimensions, mazes with islands, reliance on physical realignment in addition to encoders, and the absence of turn-optimized shortest-path planning. See [limitations](docs/NAVIGATION_AND_LIMITATIONS.md).

## Reproducing the project

Open `src/MazeSolverPhysical.c` in a ROBOTC environment compatible with LEGO EV3 and configure the hardware as documented. Update `robHeading`, `robRow`, `robCol`, `targetRow`, and `targetCol` in the source to match the test maze before deployment. **The archived source has not been independently compiled or hardware-retested for this GitHub publication.** This is an academic archive, not a turnkey simulation or tested release.

## Project attribution and provenance

This was a **group project (Group 17)**, not an individual-only build. The source preserves the original group's program structure; sensitive student identification numbers have been removed. The university assignment handout and an unformatted intermediate backup are retained outside this public repository. No third-party EV3 firmware or proprietary ROBOTC tooling is bundled.

## Portfolio

**Hasan Fairuz** — Mechatronic Systems Engineering

[Engineering Portfolio](https://hasanfairuz.com/) · [GitHub Profile](https://github.com/HasanFairuz)
