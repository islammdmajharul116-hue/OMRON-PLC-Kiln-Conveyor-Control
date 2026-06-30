# Safety Interlocks

This document describes the safety interlock logic for the OMRON PLC kiln conveyor unloading simulation.

## Safety Conditions Required

The conveyor motor is only allowed to run when all of the following conditions are true:

- Emergency stop is released
- Safety door or guard is closed
- Motor overload is healthy
- Temperature is below the critical shutdown limit
- No conveyor jam fault is active
- No latched system fault is active

## Master Safety Logic

```text
SYSTEM_SAFE =
    E_STOP_OK
    AND SAFETY_DOOR_CLOSED
    AND MOTOR_OVERLOAD_OK
    AND NOT TEMP_CRITICAL
    AND NOT JAM_FAULT
    AND NOT FAULT_LATCHED
