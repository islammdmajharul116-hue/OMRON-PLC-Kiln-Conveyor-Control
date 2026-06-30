# System Diagram

Text-based system diagram for the OMRON PLC kiln conveyor unloading control project.

```text
+-----------------------+
|   High Temp Kiln      |
|   Ceramic Products    |
+----------+------------+
           |
           | Unload Request
           v
+-----------------------+        +----------------------+
| Kiln Unloading Zone   |------->| Conveyor System      |
| Entry Sensor          |        | Motor + Exit Sensor  |
+----------+------------+        +----------+-----------+
           |                                |
           | Sensor Feedback                | Product Clear Signal
           v                                v
+-------------------------------------------------------+
|                    OMRON PLC                          |
|                                                       |
| Inputs: E-Stop, Door Switch, Entry/Exit Sensors,      |
| Temp Sensor, Start/Stop/Reset, Motor Overload         |
|                                                       |
| Outputs: Conveyor Motor, Alarm Light, Horn,           |
| Ready Light, Unload Complete Signal                   |
+-------------------------+-----------------------------+
                          |
                          v
+-------------------------------------------------------+
| Safety and Fault Logic                                |
| E-Stop | Door Open | Over Temp | Jam | Overload       |
+-------------------------------------------------------+
```

## Control Flow

1. Kiln unload request is received.
2. PLC verifies all safety conditions.
3. Conveyor motor starts when the system is safe.
4. Entry and exit sensors track product movement.
5. Thermal sensor monitors high-temperature condition.
6. Fault logic stops the conveyor during unsafe operation.
7. Operator reset is required after latched faults.
