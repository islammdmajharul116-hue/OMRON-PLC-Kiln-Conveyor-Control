# Simulation Test Cases

This document defines test cases for validating the OMRON PLC kiln conveyor unloading simulation.

## Test Case 1: Normal Automatic Cycle

**Condition:** Auto mode is selected, all safety inputs are healthy, and unload request is active.  
**Expected Result:** Conveyor starts, product moves from entry sensor to exit sensor, unload complete signal turns on, and system returns to idle.

## Test Case 2: Emergency Stop During Movement

**Condition:** Emergency stop is pressed while conveyor is running.  
**Expected Result:** Conveyor motor turns off immediately, alarm light turns on, and restart is blocked until reset.

## Test Case 3: Safety Door Opened

**Condition:** Safety door opens during automatic unloading.  
**Expected Result:** Conveyor stops, system safe bit turns off, and auto cycle is interrupted.

## Test Case 4: Over-Temperature Shutdown

**Condition:** Thermal sensor value rises above the critical limit.  
**Expected Result:** Conveyor is inhibited, alarm is latched, and restart is allowed only after temperature returns to safe range.

## Test Case 5: Conveyor Jam Detection

**Condition:** Entry sensor detects product, but exit sensor does not detect product before timer expires.  
**Expected Result:** Jam fault activates, conveyor stops, alarm light turns on, and manual reset is required.

## Test Case 6: Motor Overload Fault

**Condition:** Motor overload healthy signal turns off.  
**Expected Result:** Conveyor motor command turns off and fault latch is activated.

## Test Case 7: Sensor Failure

**Condition:** Sensor feedback does not match expected conveyor sequence.  
**Expected Result:** PLC stops the sequence and activates a sensor fault/alarm condition.

## Test Case 8: Reset After Fault

**Condition:** Fault condition is cleared and reset pushbutton is pressed.  
**Expected Result:** Fault latch clears only when all safety conditions are healthy.
