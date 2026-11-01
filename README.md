README — AUTOMATED STORAGE AND RETRIEVAL SYSTEM
Factory I/O + CONTROL I/O

-1. PROJECT PURPOSE

This project simulates an automated warehouse with:
- Three stacker cranes.
- Two storage groups containing three racks each.
- 54 storage positions per group, or 108 positions total.
- Loading conveyors and an automatic unloading route.

L1 and L2 store incoming boxes.
The middle crane retrieves stored boxes and sends them to the exit.

-2. HOW TO START
   
1. Open Factory I/O.
2. Stop any currently running simulation.
3. Open Warehouse_Autotz.factoryio.
4. Go to File > Drivers, or press F4.
5. Select Control I/O.
6. In CONTROL I/O, open:
   Warehouse Controlz.controlio
7. Confirm that the driver is connected.
8. Keep the controller cycle at 10 ms and enable
   synchronization with the simulation.
9. Reset the Factory I/O scene and CONTROL I/O together
   so the rack contents and controller memory start clean.
10. Set the simulation time scale to 1x.
11. Select Auto.
12. Click Run in CONTROL I/O.

With the default synchronization settings, CONTROL I/O
also puts Factory I/O into Run mode.

-3. AUTOMATIC STORAGE SEQUENCE

The intended operating sequence is:

1. A palletized box enters the loading station.
2. The loading sensors confirm its arrival.
3. The assigned loading crane picks it up.
4. The crane moves to the selected rack position.
5. The forks extend and place the load on the rack.
6. The forks retract before the crane travels again.
7. The controller records the completed storage operation.
8. The next box is released after storage is completed.

The loading cranes alternate storage operations.
Storage begins at the programmed farthest, upper position
and follows the controller's position order.

-4. AUTOMATIC RETRIEVAL SEQUENCE

The current control design permits a new retrieval when
BOTH storage groups contain at least 27 stored boxes.

This threshold is checked before each new retrieval.
The system does not need to fill all 108 positions first.

The middle crane follows FIFO:
FIRST IN, FIRST OUT.

This means the oldest stored box is retrieved first.

The intended unloading sequence is:

1. Select the oldest stored box.
2. Move the middle crane to its rack position.
3. Pick up the box and retract the forks.
4. Return to the unloading position.
5. Place the box on the receiving conveyor.
6. Retract the forks.
7. Start the receiving and curved conveyors.
8. Carry the box through the rear exit conveyors.
9. Confirm passage at the exit sensor.
10. Continue the storage and retrieval loop.

-5. MIDDLE UNLOADING ROUTE
   
Middle crane
> Receiving conveyor with fork clearance
> One free roller
> Clockwise curved roller conveyor
> Straight exit conveyors
> Exit sensor
> Remover

The free roller is passive and has no motor command.

The curved conveyor uses the actuator:
M Exit Curve CW

The receiving and curved conveyors must remain stopped
during placement and begin discharging after fork retraction.

-6. PAUSE, RESUME, STOP, AND RESET

PAUSE:
Use Pause for temporary inspection.
Confirm that both the controller and simulation pause.

RESUME:
Resume through CONTROL I/O and check that both applications
continue together.

STOP:
Stop the simulation and controller before changing the
layout, wiring, or actuator settings.

RESET:
Reset both applications together to begin a fresh cycle.
Do not reset only the controller while leaving stored boxes
in the racks; its inventory memory could become inconsistent
with the scene.

TIME SCALE:
Begin testing at 1x.
Check transfers at normal speed before testing other speeds.
Do not assume faster simulation speeds preserve pallet stability.
