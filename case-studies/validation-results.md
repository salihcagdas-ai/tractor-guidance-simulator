# What did the simulator and the cab computer actually pass?

In the physics model, eight of twelve tractor scenarios finished. Four handed control back to the operator. On the Raspberry Pi, two interrupted jobs recovered their original routes after a reboot. Those experiments answer different questions about the same system.

## Can the tractor model follow the route?

On November 19, 2026, the tractor ran through twelve scenarios in Project Chrono, a vehicle dynamics simulator.

| Conditions | Outcome |
| --- | --- |
| Straight travel, turning, wheel slip, sensor fault | All four reference scenarios finished and met their software criteria. |
| Field travel, field turn, rough surface, vegetation | All four scenarios finished. |
| Mud, sloping soil, mixed soil, different grip on the left and right wheels | All four ended in an operator handover when the controller could no longer validate tracking. The slope run also exceeded its permitted deviation from the route. |

The four unfinished runs are open calibration cases. Tire grip and soil response still need field measurements. The separate [implement coverage comparison](field-coverage.md) measures the area swept in a geometric replay.

## How long did it take to withdraw steering permission?

On November 19, I tested the control software with a simulated motor link and protection circuit. The clock starts when the fault is introduced and stops when the model withdraws permission to steer.

| Change in the simulation | Result |
| --- | --- |
| Position corrections interrupted for 0.8 s | Permission stayed on while the last correction was still fresh. |
| Position corrections interrupted for 4 s | Permission cut after 2.010 s. |
| Motor feedback stopped, or outgoing motor commands stopped getting through | Permission cut after 80 ms in each direction. |
| Controller froze with its ready signal still high | The independent watchdog cut permission after 122 ms. |
| Cab restarted | Permission cut after 300 ms. |

Across all ten cases, eight caused a cutoff. All eight stayed disabled until the simulated operator explicitly rearmed the system. These times measure the software and circuit model. Relay opening time, steering-wheel release and stopping distance require physical tests.

## What ran on a physical Raspberry Pi?

- **November 13, 2026 — restart during fieldwork.** The spreader job was paused and the sprayer job was running when the Pi rebooted. Both returned paused, with the saved route, position, elapsed time and worked area intact. Each finished when resumed.
- **November 15, 2026 — conflicting position and speed.** A physical Pi 5 processed 312 simulated runs across 13 conditions. The GPS-only check missed a combined position and speed fault in all 24 corresponding runs. With independent movement checks, steering permission was cut in all 24, after 1.82–4.70 s. The 24 healthy runs had zero false cutoffs. An offset present from startup remained undetected. [Sensor experiment and stopping limits](position-integrity.md)

## Software regression results

The November 19 release report records each test group separately.

| Test group | Recorded result |
| --- | --- |
| Python simulation and quality checks | 515 passed, zero skipped |
| Node.js cab, web, home application, packaging and steering checks | 109 passed, zero skipped |
| RTK positioning and correction-data tools | 136 passed, zero skipped |
| Protection circuit model and steering permission | 39 passed, zero skipped |

For this portfolio update I reran the steering checks on Windows. Two Python integration tests exercised the ten modeled cases, and nine Node.js tests checked stale or invalid inputs, pause, recovery and restart. All eleven tests passed. This was a focused repeat of checks from the release suites.

[Back to Tractor Guidance Simulator](../README.md)
