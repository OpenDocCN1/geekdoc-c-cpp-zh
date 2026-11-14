+   - The frequencies are fixed but span a range of values.
+   - The time intervals span a range of values and may be either periodic or aperiodic, but they cannot be both.
+   - The counter will support the user's ability to manually select mode and measurement range for all input signals.
+   - The counter will continue to make and display the selected attribute of the signal until power to the system is turned off or until the user makes another selection.
+   - The counter will measure only one signal at a time.
+   - An event can be modeled as an aperiodic time signal.
+   - The design will be sufficiently flexible to allow future inclusion of the ability to send commands from a computer to the counter to direct its operation.
+   - The response of the counter to remote commands will be the same as its response to front panel selections, with the exception that measured data will be sent from the counter to the computer as well as to the front panel display.

# System Requirements Specification

The next step is to formalize, in a specification, what is known about the system to be designed. The document, the System Requirements Specification, opens with a summary of the design.

# System Requirements Specification for a Digital Counter

# System Description

This specification describes and defines the basic requirements for a digital counter. The counter is to be able to measure frequency, period, time interval, and events. The system supports three measurement ranges for each signal and two for events. The counter is to be manually operated with the ability to support remote operation in future. The counter is to be low cost and flexible, so that it may be utilized in a variety of applications.

# Specification of External Environment

The counter is to operate in an industrial environment in a commercial grade temperature and lighting environment. The unit will support either line power or battery operation.

# System Input and Output Specification

# System Inputs

The system shall be able to measure the following signals.

# Frequency in Three Ranges

+   - High range up to 150.000 MHz
+   - Mid-range up to 50.000 KHz
+   - Low range up to 100.000 kHz

# Period in Three Ranges

+   - High resolution up to 1.0000 ms
+   - Mid-resolution up to 10.000 ms
+   - Low resolution up to 1.000 s

# Time Interval in Three Ranges

+   - High resolution up to 1.0000 ms
+   - Mid-resolution up to 10.00 ms
+   - Low resolution up to 1.000 s
+   - Voltage range 0.0-4.5 VDC

# Events - Up to 99 events in one minute

+   All signal inputs will be:
+   - Digital data
+   - Voltage range 0.0-4.5 VDC

# System Outputs

The system shall measure and display the following signals using a 6-digit display.

# Frequency in Three Ranges

+   - High range up to 200.000 ± 0.001 MHz
+   - Mid-range up to 200.000 ± 0.001 KHz
+   - Low range up to 200.000 ± 0.001 Hz

# Period in Three Ranges

+   - High resolution up to 2.000 ± 0.0001 ms
+   - Mid-resolution up to 20.00 ± 0.01 ms
+   - Low resolution up to 2.000 ± 0.001 s