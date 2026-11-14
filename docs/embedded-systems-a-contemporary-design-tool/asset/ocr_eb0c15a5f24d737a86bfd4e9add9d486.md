# 8.11.3 Data Faults and the Communications Subsystem

The communications subsystem brings commands and data into the system from the external world and/or sends the same in the other direction. Corrupted information can jeopardize the safety, security, reliability, and robustness of the system. Of initial concern is the ability to distinguish between valid and corrupted data. Thereafter, any erroneous information must be dealt with either by correcting the error or utilizing the exchange protocol or an encoding algorithm.

# 8.11.4 Power and Reset Subsystems

Both the main control function and the alarm subsystem require power to operate. As with the alarm subsystem, one should avoid designs that utilize the same power system for both the command and the alarm functions. Often, when designing a safety critical system, the safety/alarm components are powered by an uninterruptible power supply (UPS). Thus, if the power subsystem for the main system fails, the alarm capability remains operational. One could also design an alarm monitoring system into the main system. Failure of the power supply for the alarm and shutdown subsystem could trigger a compromised state alarm via the main system. If the design utilizes a common power system, the potential for a single-point failure exists and can be a significant problem.

# *Power On Reset (POR)*

Every system should have a *Power On Reset (POR)* capability to ensure that all the comprising storage elements start in a known state. A common reset to the two major blocks of the system prevents either from doing its job. The main block and the safety critical block should each have a POR from its own supply.

# 8.11.5 Peripheral Device Subsystems

Hard or soft failures in any of the peripheral devices can affect the operation of the application in a number of ways. A hard failure in any device eliminates the services it was intended to provide. A soft failure, in which the device appears to be functioning but is actually returning incorrect data or performing an incorrect operation, potentially raises a higher safety risk. Either failure presents two problems: identifying the occurrence of the fault and dealing with the consequences. Identifying the fault can be addressed through built-in self-test functions running in the background. Coping with the loss of a (critical) device is a design phase issue that is dealt with in the same manner as the control and alarm faults.

# 8.11.6 Clock Subsystem

System designs that utilize the same clock or time base for both command and alarm functions have a potential common point for failure. In the system described earlier, both the main control function and the watchdog subsystem require a clock to operate. A watchdog timer is like the *dead man's throttle* on a train. If not reset on a regular basis, the watchdog timer forces the system into a fail-safe state. If a shared clock is used, failure of the clock prevents the microprocessor from resetting the watchdog timer. At the same time, such a failure also prevents the timer from advancing. Independent clocks, similar to independent microprocessors, mitigate the effect of the simultaneous failure of two clocks.

# *dead man's throttle*

We will now examine each of these pieces of functionality and present system-level alternatives for supporting robust and reliable designs while reducing safety risks. One