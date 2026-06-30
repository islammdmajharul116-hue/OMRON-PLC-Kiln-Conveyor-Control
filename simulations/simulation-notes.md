# Simulation Notes

This document explains how the kiln conveyor PLC logic can be simulated and tested.

## Simulation Purpose

The simulation validates the control behavior of a kiln conveyor unloading system before applying similar logic to a real PLC environment. The goal is to test system response during normal operation, safety events, and fault conditions.

## Simulated Inputs

| Input | Simulation Action |
|---|---|
| E_STOP_OK | Toggle emergency stop healthy/pressed condition |
| SAFETY_DOOR_CLOSED | Toggle safety guard open/closed |
| AUTO_MODE | Enable automatic sequence |
| START_PB | Start the automatic unload cycle |
| STOP_PB | Stop the conveyor |
| RESET_PB | Reset latched faults after safe conditions return |
| ENTRY_SENSOR | Simulate product entering conveyor |
| EXIT_SENSOR | Simulate product leaving conveyor |
| TEMP_SENSOR | Adjust temperature value |
| MOTOR_OVERLOAD_OK | Simulate motor overload trip |

## Simulated Outputs

| Output | Expected Behavior |
|---|---|
| CONVEYOR_MOTOR_RUN | Turns on during safe active unload sequence |
| ALARM_LIGHT | Turns on during fault condition |
| HORN | Turns on during critical or latched fault |
| READY_LIGHT | Turns on when system is ready |
| UNLOAD_COMPLETE | Turns on after product exits conveyor |

## Normal Test Flow

1. Set emergency stop healthy.
2. Close safety door.
3. Set motor overload healthy.
4. Set temperature below warning limit.
5. Select auto mode.
6. Press start.
7. Activate unload request.
8. Trigger entry sensor.
9. Trigger exit sensor.
10. Confirm unload complete signal.

## Fault Test Flow

1. Start conveyor in auto mode.
2. Activate entry sensor.
3. Do not activate exit sensor.
4. Allow jam timer to complete.
5. Confirm jam fault activates.
6. Confirm conveyor stops.
7. Clear fault condition.
8. Press reset.
9. Confirm system can restart only after safe conditions return.

## Expected Learning Outcome

This simulation demonstrates PLC sequencing, interlock design, analog temperature monitoring, conveyor jam detection, and safe restart behavior.
