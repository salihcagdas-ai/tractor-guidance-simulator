# What if the tractor trusts the wrong position?

A receiver that stops sending updates is easy to spot. A harder case is a receiver that keeps reporting a plausible speed and a matching change in position while both are wrong. The marker on the map keeps moving. Did the wheels actually cover that distance?

I tested this on a **Raspberry Pi 5 in 312 simulation runs**. For each of 13 conditions, I ran the roller, spreader and sprayer in both straight travel and turns, with four sensor-noise samples for each combination. That gave 24 runs per condition. The cab computer was a physical Pi. Software generated the tractor motion and sensor readings.

## When did the simulator disable steering?

| Condition | Runs with steering disabled | Time from fault onset to cutoff |
| --- | ---: | --- |
| Normal operation | 0 / 24 | No false alarms |
| GPS updates stopped | 24 / 24 | 0.46–0.54 s |
| GPS readings froze | 24 / 24 | 0.46–0.54 s |
| Position and speed both wrong, checked against GPS alone | 0 / 24 | Fault went undetected |
| Same fault, checked against the inertial measurement unit (IMU), wheel speed and steering angle | 24 / 24 | 1.82–4.70 s |

The GPS-only check accepted the faulty data because the reported speed agreed with the change in position. With independent motion measurements, the system detected the discrepancy in every run. The slowest detection took **4.70 seconds**. Detection time on the tractor is still to be measured.

**A position error from startup can persist.** Imagine the map puts the tractor one row over at startup, then tracks every subsequent meter and turn accurately. The wheels and IMU still agree with the movement on the map. The simulated checks missed this constant offset. Verifying the starting position requires a reference with an independently known location.

**Does cutting steering stop the tractor?** When I removed the simulated driver's brake intervention, the tractor model kept moving in all **48 runs**, even after steering commands stopped. Braking, stopping distance and manual steering takeover still need to be tested on the vehicle.

## Where does a job resume after a Pi restart?

In a separate experiment I opened two job records on the cab computer. The fertilizer job was paused and the spraying job was running when the Pi restarted. Both came back **paused**. For each one, I compared the restored route, position along the pass, elapsed time and worked area with their values before shutdown. Both records matched. After the operator resumed each job, it finished on its original route.

[Back to Tractor Guidance Simulator](../README.md)
