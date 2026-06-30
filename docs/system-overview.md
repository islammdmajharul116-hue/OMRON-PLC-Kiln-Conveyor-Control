# System Overview

This document describes the OMRON PLC-based kiln conveyor unloading control system.

## Process Summary

The system controls the movement of ceramic products from a high-temperature kiln unloading area onto a conveyor. Before the conveyor is allowed to run, the PLC checks safety devices, temperature feedback, motor status, and sensor conditions.

## Main Equipment

- OMRON PLC controller
- Kiln unloading station
- Conveyor motor
- Entry sensor
- Exit sensor
- Thermal sensor
- Emergency stop
- Safety door switch
- Alarm indicator
- Reset pushbutton

## Operating Modes

### Manual Mode

Manual mode allows controlled testing of the conveyor when all safety conditions are healthy.

### Auto Mode

Auto mode runs the unloading sequence automatically after the kiln unload request is active and all safety interlocks are satisfied.

## Safety Philosophy

The conveyor motor can only run when the system is safe. Any emergency stop, open guard, over-temperature condition, motor overload, or jam fault will stop the conveyor and block restart until the issue is cleared.
