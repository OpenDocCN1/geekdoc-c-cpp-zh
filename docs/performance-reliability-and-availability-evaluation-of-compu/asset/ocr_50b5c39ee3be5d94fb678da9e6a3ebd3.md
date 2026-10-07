# Fault Injection and Failure Monitoring 627

The collection module is used to observe the target system. Finally, the management module is accountable for the automated and parameterizable generation of the test sequences, controlling the execution runtime, and storing the result for post-test analysis. The first three modules are hardware modules, whereas the management module is implemented as a software component [19, 20].

+   - RIFLE

RIFLE is a hardware fault injection mechanism that injects faults at the pin-level of hardware modules such as the processor, the bus, controllers, or other devices. The injection of faults is deterministic and can be reproduced if required. RIFLE can also detect particular states in which the faults do not harm the target system. The preeminent idea of RIFLE is to trigger and tracing methods adopted in digital logic analyzers with the logic demanded by the pin-level fault insertion. The tracing data is adopted for describing faults and their influence on the target system and for error propagation analysis [250].

+   - DEFINE

DEFINE is a distributed fault injection and monitoring environment to evaluate system dependability, analyze fault propagation, and validate fault-tolerant mechanisms. DEFINE can inject hardware faults (emulation) and software faults into a distributed system and observe their impact and propagation among mechanisms. It applies two fault injection methods: the first employs the hardware that interrupts to control fault injection and activation; the second adopts software traps to inject and monitor fault activation. DEFINE consists of four parts: a controller, a software monitor, a fault injector, and a workload generator. A target system is a group of connected machines. Therefore, DEFINE should be installed on a machine that is not part of the target system for not being affected by the faults [458].

+   - MEISTO-C

MEISTO-C [144] is an upgraded version of MEISTO (Multi-level Error/Fault Injection Simulation Tool) [192]. MEISTO-C uses a VHDL simulator for injecting faults via simulator commands that alter variables and signals defined in VHDL models. It grants users a set of predefined model faults, features to set up and control fault attacks. MEISTO-C supports estimating fault-tolerance mechanisms' coverage, investigating VHDL abstraction-level mappings, and validating fault-tolerant mechanisms.

+   - FERRARI

The Fault and ERror Automatic Real-time Injector (FERRARI) is a software fault injection tool that simulates transient errors and permanent hardware faults by corrupting the executing program's state. This is accomplished by using traps and system calls to enable software to emulate the effects of faults and errors. One of FERRARI's key features is to support the type, location, and