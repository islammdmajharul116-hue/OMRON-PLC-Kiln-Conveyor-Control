# PLC I/O Mapping

This document lists the example PLC input and output signals used in the kiln conveyor unloading simulation.

## Digital Inputs

| Address | Signal Name | Device | Description |
|---|---|---|---|
| 0.00 | E_STOP_OK | Emergency Stop | Healthy when emergency stop is released |
| 0.01 | SAFETY_DOOR_CLOSED | Safety Door Switch | Confirms guard or door is closed |
| 0.02 | AUTO_MODE | Mode Selector | Enables automatic unloading sequence |
| 0.03 | MANUAL_MODE | Mode Selector | Enables manual conveyor testing |
| 0.04 | START_PB | Start Pushbutton | Starts system when safe |
| 0.05 | STOP_PB | Stop Pushbutton | Stops conveyor command |
| 0.06 | RESET_PB | Reset Pushbutton | Clears latched faults after safe condition |
| 0.07 | ENTRY_SENSOR | Photoelectric Sensor | Detects product entering conveyor |
| 0.08 | EXIT_SENSOR | Photoelectric Sensor | Confirms product exits conveyor |
| 0.09 | MOTOR_OVERLOAD_OK | Motor Protection | Healthy when overload is not tripped |
| 0.10 | UNLOAD_REQUEST | Kiln Signal | Requests product unloading from kiln area |

## Analog Inputs

| Address | Signal Name | Device | Description |
|---|---|---|---|
| A0 | TEMP_SENSOR | Thermal Sensor | Measures kiln unloading zone temperature |

## Digital Outputs

| Address | Signal Name | Device | Description |
|---|---|---|---|
| 100.00 | CONVEYOR_MOTOR_RUN | Motor Contactor | Runs conveyor motor |
| 100.01 | ALARM_LIGHT | Alarm Tower Light | Indicates active fault |
| 100.02 | UNLOAD_COMPLETE | Status Signal | Indicates unloading cycle complete |
| 100.03 | READY_LIGHT | Status Light | Indicates system ready |
| 100.04 | HORN | Audible Alarm | Sounds during critical fault |

## Internal PLC Bits

| Tag | Description |
|---|---|
| SYSTEM_SAFE | All safety conditions are healthy |
| AUTO_CYCLE_ACTIVE | Automatic unload sequence is running |
| JAM_FAULT | Conveyor jam condition is active |
| TEMP_WARNING | Temperature is above warning threshold |
| TEMP_CRITICAL | Temperature is above critical shutdown threshold |
| FAULT_LATCHED | A fault is stored until reset |
