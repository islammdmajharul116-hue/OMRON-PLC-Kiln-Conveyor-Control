# Ladder Logic Safety Interlock Simulation

This document represents the safety interlock logic in ladder-style form for the OMRON PLC kiln conveyor unloading system.

## Ladder Logic Rungs

```text
|----[ E_STOP_OK ]----[ SAFETY_DOOR_CLOSED ]----[ MOTOR_OVERLOAD_OK ]----[/ TEMP_CRITICAL ]----[/ JAM_FAULT ]----( SYSTEM_SAFE )----|

|----[ SYSTEM_SAFE ]----[ AUTO_CYCLE_ACTIVE ]----[/ STOP_PB ]----( CONVEYOR_MOTOR_RUN )----|

|----[/ E_STOP_OK ]------------------------------------------------( E_STOP_FAULT )----|

|----[ E_STOP_FAULT ]----------------------------------------------( FAULT_LATCHED )----|

|----[/ SAFETY_DOOR_CLOSED ]---------------------------------------( SAFETY_DOOR_FAULT )----|

|----[/ MOTOR_OVERLOAD_OK ]----------------------------------------( MOTOR_OVERLOAD_FAULT )----|

|----[ FAULT_LATCHED ]---------------------------------------------( ALARM_LIGHT )----|

|----[ FAULT_LATCHED ]---------------------------------------------( HORN )----|

|----[ RESET_PB ]----[ E_STOP_OK ]----[ SAFETY_DOOR_CLOSED ]----[ MOTOR_OVERLOAD_OK ]----[/ TEMP_CRITICAL ]----( RESET_ALLOWED )----|
```

## Logic Explanation

The master safety rung creates the `SYSTEM_SAFE` permission only when all required safety conditions are healthy. The conveyor motor can run only when the system is safe, auto cycle is active, and the stop pushbutton is not active.

Fault conditions are latched so the system does not restart automatically after an unsafe event. The operator must clear the unsafe condition and press the reset pushbutton before restarting.

## Safety Conditions

- Emergency stop must be released
- Safety door or guard must be closed
- Motor overload must be healthy
- Temperature must be below the critical limit
- Jam fault must not be active
- Fault latch must be cleared before restart

## Notes

This ladder logic is written in text format to document the control behavior. In a real OMRON PLC environment, the same logic would be implemented using ladder contacts, coils, timers, and internal memory bits.
