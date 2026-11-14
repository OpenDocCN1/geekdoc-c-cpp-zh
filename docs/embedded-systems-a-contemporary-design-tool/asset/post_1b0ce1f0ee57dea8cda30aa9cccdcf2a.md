
The security considerations should address:

- Potential vulnerabilities.
- Potential pre-, during, and post-attack defense strategies.

With respect to reliability, one can specify:

- The system uptime goals.
- Potential risks, failures, and failure modes.
- Failure management strategy.

## Example 9.1 IDENTIFYING THE REQUIREMENTS

### Designing a Counter (cont.)

Starting from the trip report from High Flying Avionics, Inc., which discussed its needs for a new counter, let's put the requirements specification together.

As a first step in the thought process, one extracts and summarizes the essential information from the trip report. By doing so, one can begin to focus on what should be included in the requirements specification. From the discussions with the customer, a high-level sketch of the system and the environment captures the essential parts of the problem. The next step is to begin to formalize the model of the system and the environment, as illustrated in Figure 9.24. Let's put the Requirements Specification together.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_494_0.png)

### Figure 9.24 The System and Its Environment – Step 2

In its initial configuration, the environment contains:

- A set of navigation radios that are to be tested.
- The user who is doing the testing.
- The factory.

Signals flow from the navigation radio to the counter, but not the reverse. The factory has inputs to the counter as well; these include the power system and the ambient environment in the factory. The user interaction is bidirectional. The user must select and configure the measurement to be made and then view the results once the measurement is complete. For the computer, the signal interchange with the counter similarly occurs in both directions.

In the developing model, the factory can be viewed as an aggregation of test lines and the radios to be tested. Later, the remote computer is to be added. The system to be designed, that is, the counter, interacts with all three entities. Such an interaction is reflected in Figure 9.25.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_495_0.png)

### Figure 9.25 The System as an Aggregation of Components

Now let's move to the next level of detail.

### The Environment

- The customer has stated that the counter is to operate in a factory environment on any of several production lines. Based on such an understanding, one can make certain assumptions about temperature, power, and ambient lighting.
- Time intervals and frequencies on the navigation radios and events from equipment monitoring the production line are to be measured.
- The time intervals may be either periodic or aperiodic but cannot be both.
- The polarity of the event signal to be counted can be either positive or negative going.
- The data display and the annunciation for mode and range are the only outputs expected from the counter.
- The assumption is made that the signals to be measured are independent of one another.
- In future, commands will be sent from a computer to the counter to direct its operation. Data will be sent from the counter to the computer.

### The Counter

- The counter must have the ability to measure time intervals and frequencies and to count events.
- The frequencies are fixed but span a range of values.
- The time intervals span a range of values and may be either periodic or aperiodic, but they cannot be both.
- The counter will support the user's ability to manually select mode and measurement range for all input signals.
- The counter will continue to make and display the selected attribute of the signal until power to the system is turned off or until the user makes another selection.
- The counter will measure only one signal at a time.
- An event can be modeled as an aperiodic time signal.
- The design will be sufficiently flexible to allow future inclusion of the ability to send commands from a computer to the counter to direct its operation.
- The response of the counter to remote commands will be the same as its response to front panel selections, with the exception that measured data will be sent from the counter to the computer as well as to the front panel display.

### System Requirements Specification

The next step is to formalize, in a specification, what is known about the system to be designed. The document, the System Requirements Specification, opens with a summary of the design.

### System Requirements Specification for a Digital Counter

### System Description

This specification describes and defines the basic requirements for a digital counter. The counter is to be able to measure frequency, period, time interval, and events. The system supports three measurement ranges for each signal and two for events. The counter is to be manually operated with the ability to support remote operation in future. The counter is to be low cost and flexible, so that it may be utilized in a variety of applications.

### Specification of External Environment

The counter is to operate in an industrial environment in a commercial grade temperature and lighting environment. The unit will support either line power or battery operation.

### System Input and Output Specification

### System Inputs

The system shall be able to measure the following signals.

### Frequency in Three Ranges

- High range up to 150.000 MHz
- Mid-range up to 50.000 KHz
- Low range up to 100.000 kHz

### Period in Three Ranges

- High resolution up to 1.0000 ms
- Mid-resolution up to 10.000 ms
- Low resolution up to 1.000 s

### Time Interval in Three Ranges

- High resolution up to 1.0000 ms
- Mid-resolution up to 10.00 ms
- Low resolution up to 1.000 s
- Voltage range 0.0-4.5 VDC

### Events - Up to 99 events in one minute

- All signal inputs will be:
  - Digital data
  - Voltage range 0.0-4.5 VDC

### System Outputs

The system shall measure and display the following signals using a 6-digit display.

### Frequency in Three Ranges

- High range up to 200.000 ± 0.001 MHz
- Mid-range up to 200.000 ± 0.001 KHz
- Low range up to 200.000 ± 0.001 Hz

### Period in Three Ranges

- High resolution up to 2.000 ± 0.0001 ms
- Mid-resolution up to 20.00 ± 0.01 ms
- Low resolution up to 2.000 ± 0.001 s

### Time Interval in Three Ranges

- High resolution up to 2.0000 ± 0.0001 ms
- Mid-resolution up to 20.00 ± 0.01 ms
- Low resolution up to 2.000 ± 0.001 s

### Events in Two Ranges

- Fast up to 200 events in one minute
- Slow up to 2000 events in one hour

### User Interface

The user shall be able to select the following using buttons and switches on the front panel of the instrument.

| Setting | Options |
|---------|---------|
| Mode | Frequency, Period, Time Interval, Events |
| Range | Frequency, Period, Time Interval – High, Mid, Low; Events – Fast, Slow |
| Trigger Edge (Frequency, Period, and Events) | Rising or falling edge |
| Trigger Edge (Time Interval) | Rising to rising edge; Falling to falling edge; Rising to falling edge; Falling to rising edge |
| Reset | |
| Power ON/OFF | |

The measurement results will be presented on a 6-digit display; leading zeros will be suppressed. The display shall be readable in direct sunlight and from any angle.

The front panel will appear as follows.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_497_0.png)

### Use Cases

The use cases for the counter are given in the following two diagrams.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_497_1.png)

The first indicates manual operation through the front panel and the second through a remote connection to a computer.

The remote option will not be included in the initial model but will be incorporated in a later release. The time that of release is to be determined.

Execution of the selected measurement function will not depend on how (local or remote) that function was selected.

At power ON, the default mode is to measure frequency. All ranges will default to their highest value.

### Measure Frequency

The counter will continuously measure and display the frequency of the input signal on the currently selected range as long as the Frequency mode is selected.

If the frequency of the input signal exceeds the maximum allowable value on the selected range, the display will present the full-scale reading and will flash.

If the frequency of the input signal is below the minimum allowable value on the selected range, the display will present a zero reading.

If the input signal returns to a value within the bounds of the range, the value of the frequency will be displayed.

The range may be changed at any time by depressing the range select push button.

The user may elect to measure frequency starting on the positive or negative edge of the signal by depressing the start trigger edge push button.

### Measure Period

The counter will continuously measure and display the period of the input signal on the currently selected range as long as the Period mode is selected.

If the period of the input signal exceeds the maximum allowable value on the selected range, the display will present the full-scale reading and will flash. If the period of the input signal is below the minimum allowable value on the selected range, the display will present a zero reading.

If the input signal returns to a value within the bounds of the range, the value of the period will be displayed.

The range may be changed at any time by depressing the range select push button.

The user may elect to measure a period starting on the positive or negative edge of the signal by depressing the start trigger edge push button.

### Measure Interval

The counter will continuously measure and display the duration of the selected portion of the input signal on the currently selected range as long as the Interval mode is selected.

If the duration of the selected portion of the input signal exceeds the maximum allowable value on the selected range, the display will present the full-scale reading and will flash.

If the duration of the selected portion of the input signal is below the minimum allowable value on the selected range, the display will display zero.

If the input signal returns to a value within the bounds of the range, the value of the duration of the selected portion of the input signal will be displayed.

The range may be changed at any time by depressing the range select push button.

The user may elect to commence measuring the interval on the positive or negative edge of the signal by depressing the start trigger edge push button.

The user may elect to terminate the measurement interval on the positive or negative edge of the signal by depressing the stop trigger edge push button.

Note that the signal duration from positive edge to positive edge or negative edge to negative edge is the same as the period of the signal.

### Events

The counter will continuously count and display the number of occurrences of the input signal on the currently selected range. The accumulated count will be reset to 0 at the end of the select count duration.

The range may be changed at any time by depressing the range select push button.

The user may elect to increment the count on the positive or negative edge of the input signal by depressing the start trigger edge push button.

If the number of accrued counts exceeds the maximum allowable value on the selected range, the display will present the full-scale reading and will flash.

### System Functional Specification

The system is intended to make four different kinds of digital measurement in the time and frequency domains comprising frequency, period, time interval, and events. The activities associated with the measure frequency mode are shown in the following diagram.
