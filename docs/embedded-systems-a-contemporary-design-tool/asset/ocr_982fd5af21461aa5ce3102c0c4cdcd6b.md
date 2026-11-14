Input Subsystem The input subsystem shall provide the ability for the user to select any of the measurement functions, ranges, and triggering polarities. The subsystem also selects and routes the input signal to the appropriate portion of the measurement subsystem.

Output Subsystem The output subsystem implements the range, edge selection, control information, and data formatting for proper presentation on the front panel display.

Time Base The time-base subsystem is a phase locked loop and divider chain driven from a 100-MHz crystal oscillator. This subsystem will provide two clock phases to drive the internal control and decision logic. Each phase will be 200,000 ± 0.0001 MHz.

The time base will also provide the following frequencies that are used to define the measurement windows for the events and frequency measurements and provide the counting frequencies for the time interval and period measurements.

+   - Frequency – 200.0000 ± 0.0001 MHz
+   - Period – 100.0000 ± 0.0001 MHz
+   - Time Interval – 100.0000 ± 0.0001 MHz
+   - Events – 10.00 ± 0.01 Hz

Measurement Subsystem The measurement subsystem provides the logic and control to execute the measurements of time and frequency.

+   - The frequency measurement will be implemented by opening a window for 1.00 ± 0.01 seconds. During the time the window is open, the measurement subsystem will gate the unknown input frequency into a seven stage binary coded decimal (BCD) counter. When the window closes, the counter will contain the value of the unknown frequency.
+   - The activities necessary to execute a frequency measurement are given in the following diagram.
+   - The period and time interval measurements will be made by opening a window on the specified signal edge. While the window is open, a frequency of 100.0000 ± 0.0001 MHz will be gated into a seven-stage BCD counter. When the window closes, the counter will contain the values of the unknown time interval.
+   - The counter will contain the number of events that occurred during the measurement interval.
+   - The events measurement will be made by opening a window for 1.00 ± 0.01 seconds for the fast mode and 3600.0 ± 0.1 seconds for the slow mode. During the time the window is open, the measurement subsystem will gate the

unknown input to a four-stage BCD counter. When the window closes, the counter will contain a measure of the number of events that occurred during the time interval.

Power Supply Subsystem The power supply subsystem will provide the following voltages at the specified current levels to the internal logic.

+   - +5.0 ± 0.01 VDC @ 10 A
+   - +15.0 ± 0.01 VDC @ 500 mA
+   - -15.0 ± 0.01 VDC @ 500 mA

At power on, there shall be a negative going reset signal. That signal shall remain in the low state for a minimum of 10 ms and shall have the ability to sink up to 1A.

Display The instrument display shall display the results of the selected measurement on a 6-digit, 7-segment red LED display. The layout of the major features and functions is given in the earlier diagram.

# Operating Specifications

The system shall operate in a standard commercial/industrial environment.

# Temperature Range 0–85°C

Humidity up to 90% RH noncondensing Power Automatic line voltage selection

+   - 100-120 VAC ± 10% 50, 60, 400 Hz ± 10%
+   - 220-240 VAC ± 10% 50, 60 Hz ± 10%

The system shall operate for a minimum of eight hours on a fully charged battery.

Net weight: 2.75 kg, H: 90 mm x W: 200 mm x D: 300 mm

The system time base shall meet the following specifications.

# Temperature stability 0–50°C

<6 x 10^-6

# Aging Rate

90 d <3 x 10^-8
6 mo <6 x 10^-7
1 yr <25 x 10^-7

# Reliability and Safety Specification

The counter shall comply with the appropriate standards:

+   - Safety: UL-3111-1, IEC-1010, CSA 1010.1
+   - EMC: CISPR-11, IEC 801-2, -3, -4, EN50082-1

MTBF: Minimum of 10000 hours.