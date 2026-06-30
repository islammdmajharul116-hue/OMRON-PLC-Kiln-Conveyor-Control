# Conveyor Sequence Ladder Logic Simulation

This document describes the ladder-style sequence logic for the kiln conveyor unloading process.

## Sequence Rungs

```text
|----[ AUTO_MODE ]----[ START_PB ]----[ SYSTEM_SAFE ]----------------------------( AUTO_CYCLE_ACTIVE )----|

|----[ AUTO_CYCLE_ACTIVE ]----[ UNLOAD_REQUEST ]--------------------------------( STEP_10_READY )----|

|----[ STEP_10_READY ]----[ SYSTEM_SAFE ]----------------------------------------( CONVEYOR_MOTOR_RUN )----|

|----[ CONVEYOR_MOTOR_RUN ]----[ ENTRY_SENSOR ]---------------------------------( STEP_20_PRODUCT_ON_CONVEYOR )----|

|----[ STEP_20_PRODUCT_ON_CONVEYOR ]----[ EXIT_SENSOR ]--------------------------( STEP_30_PRODUCT_EXITED )----|

|----[ STEP_30_PRODUCT_EXITED ]--------------------------------------------------( UNLOAD_COMPLETE )----|

|----[ UNLOAD_COMPLETE ]---------------------------------------------------------( RESET_SEQUENCE_STEPS )----|

|----[ ENTRY_SENSOR ]----[/ EXIT_SENSOR ]----[ CONVEYOR_MOTOR_RUN ]--------------( JAM_TIMER_ENABLE )----|

|----[ JAM_TIMER_DONE ]----------------------------------------------------------( JAM_FAULT )----|
```

## Sequence Explanation

The automatic sequence starts when auto mode is active, the start pushbutton is pressed, and the system safety conditions are healthy. The PLC then waits for an unload request from the kiln area.

Once the unload request is active, the conveyor motor runs. The entry sensor confirms that product has entered the conveyor. The exit sensor confirms that the product has cleared the conveyor. After the product exits, the unload complete signal is activated and the sequence returns to idle.

## Jam Detection

A jam timer is enabled when product is detected at the entry sensor but does not reach the exit sensor while the conveyor motor is running. If the timer reaches its preset value, the PLC activates a jam fault and stops the conveyor.

## Expected Result

This sequence provides a basic simulation of conveyor movement, product tracking, unload completion, and jam detection for a kiln unloading process.
