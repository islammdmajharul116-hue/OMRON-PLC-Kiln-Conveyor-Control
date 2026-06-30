# OMRON-PLC-Kiln-Conveyor-Control

Structured Text (ST) and Ladder Logic simulation for an OMRON PLC-based high-temperature ceramic kiln conveyor unloading system.  
This project demonstrates industrial automation logic, safety interlocking, thermal feedback, conveyor fault detection, and alarm handling.

## Project Overview

This project simulates a PLC-controlled conveyor and kiln unloading process used in ceramic manufacturing. The system controls product movement from a high-temperature kiln area to an unloading conveyor while monitoring safety devices, temperature conditions, motor status, and sensor feedback.

The goal is to show practical PLC programming knowledge using structured documentation, OMRON-style logic design, and industrial control concepts.

## Key Features

- OMRON PLC-style Structured Text control logic
- Ladder Logic safety interlock documentation
- Conveyor start/stop and unload sequence logic
- Emergency stop and safety guard monitoring
- Thermal sensor feedback and over-temperature protection
- Conveyor jam detection using sensor timeout logic
- Fault latch, alarm handling, and manual reset behavior
- Simulation test cases for normal and fault conditions

## System Components

| Component | Purpose |
|---|---|
| OMRON PLC | Main controller for automation logic |
| Conveyor Motor | Moves ceramic products from kiln unloading area |
| Kiln Unload Sensor | Detects unload request or product ready condition |
| Entry Sensor | Detects product entering conveyor |
| Exit Sensor | Confirms product has cleared conveyor |
| Thermal Sensor | Monitors kiln/unload-zone temperature |
| Emergency Stop | Stops system immediately during unsafe condition |
| Safety Door Switch | Confirms guard/door is closed |
| Alarm Indicator | Shows fault or unsafe operating condition |
| Reset Pushbutton | Clears latched fault after safe condition returns |

## PLC I/O Mapping

| Signal Name | Type | Address Example | Description |
|---|---|---|---|
| E_STOP_OK | Digital Input | 0.00 | Emergency stop healthy signal |
| SAFETY_DOOR_CLOSED | Digital Input | 0.01 | Safety guard closed confirmation |
| AUTO_MODE | Digital Input | 0.02 | Auto mode selector |
| START_PB | Digital Input | 0.03 | Start pushbutton |
| STOP_PB | Digital Input | 0.04 | Stop pushbutton |
| ENTRY_SENSOR | Digital Input | 0.05 | Product detected at conveyor entry |
| EXIT_SENSOR | Digital Input | 0.06 | Product detected at conveyor exit |
| MOTOR_OVERLOAD_OK | Digital Input | 0.07 | Motor overload healthy status |
| TEMP_SENSOR | Analog Input | A0 | Kiln/unload-zone temperature feedback |
| CONVEYOR_MOTOR_RUN | Digital Output | 100.00 | Conveyor motor run command |
| ALARM_LIGHT | Digital Output | 100.01 | General alarm indicator |
| UNLOAD_COMPLETE | Digital Output | 100.02 | Cycle complete signal |

## Control Sequence

1. Operator selects Auto Mode.
2. PLC checks emergency stop, safety door, motor overload, and temperature status.
3. If all safety conditions are healthy, conveyor becomes ready.
4. Kiln unload request starts the unloading sequence.
5. Conveyor motor runs and moves product from kiln unloading area.
6. Entry and exit sensors confirm product movement.
7. If product does not reach the exit sensor within the allowed time, jam alarm activates.
8. Conveyor stops after product clears the unloading zone.
9. System returns to idle and waits for the next cycle.

## Safety Interlocks

The conveyor is only allowed to run when:

- Emergency stop is healthy
- Safety door/guard is closed
- Temperature is below critical limit
- Motor overload is healthy
- No active jam fault exists
- Reset condition has been completed after previous fault

Any unsafe condition stops the conveyor and activates an alarm.

## Fault Conditions

| Fault | System Response |
|---|---|
| Emergency stop pressed | Stop conveyor and latch alarm |
| Safety door opened | Stop conveyor and block restart |
| High temperature | Stop conveyor until temperature is safe |
| Conveyor jam | Stop motor and require manual reset |
| Motor overload | Stop system and latch fault |
| Sensor failure | Stop sequence and activate alarm |

## Simulation Test Cases

| Test Case | Expected Result |
|---|---|
| Normal auto unloading cycle | Conveyor runs and completes unload sequence |
| Emergency stop during movement | Conveyor stops immediately |
| Safety door opened | Conveyor stops and restart is blocked |
| Over-temperature condition | Conveyor inhibited until safe temperature |
| Product jam condition | Jam alarm activates after timeout |
| Motor overload fault | Motor stops and alarm latches |
| Reset after fault | System restarts only when safe conditions return |

## Repository Structure

```text
OMRON-PLC-Kiln-Conveyor-Control/
├── README.md
├── docs/
│   ├── system-overview.md
│   ├── io-map.md
│   ├── safety-interlocks.md
│   └── test-cases.md
├── st-code/
│   ├── main_control.st
│   ├── thermal_feedback.st
│   └── fault_handling.st
├── ladder-logic/
│   ├── safety_interlock_logic.md
│   └── conveyor_sequence_logic.md
├── simulations/
│   └── simulation-notes.md
└── images/
    └── system-diagram.md
```
