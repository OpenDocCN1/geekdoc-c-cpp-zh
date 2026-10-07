
## Performance, Reliability, and Availability Evaluation of Computational Systems

These leading platforms provide the grounds for more recent tools. Besides, the section also highlights a few recent appliances. Nevertheless, it does not intend to offer a comprehensive overview of present-day tools at hand; instead, it only offers relevant initiatives in the field.

- Czeck, Segall, and Siewibrek

Czeck, Segall, and Siewibre proposed a software fault insertion for embedding transient faults in the processor data path, control path, memory system, and transmission bus. The motivation for implementing such a tool was to reduce the complexity of hardware fault insertion and the respective automation processes. Besides, software inserted faults are repeatable within a system and across architectural and implementation boundaries. This tool supports defining the location, timing, and duration of the inserted faults [89].

- FIAT

The Fault-Injection-based Testing environment (FIAT) is an automated real-time distributed accelerated fault injection environment implemented to emulate hardware and software faults to support validation and uncover deficiencies in systems' error detection mechanisms, recovery procedures to guide tradeoffs between alternative designs. Faults are introduced by a fault injection library linked with the target process for corrupting memory requests from an external program. A library code is also employed to watch the process behavior and for data gathering. A solution intends to subdue the operating system's security mechanisms that prevent external processes from altering the state of a target process. FIAT also provides a user interface and a hardware/software structure for aiding the definition of workloads, faults, with means for defining fault classes, choosing where, when, and how long errors will strike, and how they will communicate with executing code or data. FIAT provides the analyst with means... for data analysis. One of the significant flaws of FIAT was linking the fault injection library at compilation time using the object or source code of the target. This procedure is unsuitable for third-party software [374, 375].

- FOCUS

FOCUS is a design automation platform for analyzing jet-engine controllers that employ a simulation environment based on SPLICE for tracking the impact of transient faults. The simulation environment feeds the analysis software with faults to discover critical design features that may lead to system failures and enable the identification of fault propagation paths and the most sensitive modules to fault propagation [75].

- MESSALINE

MESSALINE is a pin-level fault injection platform composed of four modules: the injection module, the activation module, the collection module, and the management module. The activation module assures the correct initialization of the target system.

The collection module is used to observe the target system. Finally, the management module is accountable for the automated and parameterizable generation of the test sequences, controlling the execution runtime, and storing the result for post-test analysis. The first three modules are hardware modules, whereas the management module is implemented as a software component [19, 20].

- RIFLE

RIFLE is a hardware fault injection mechanism that injects faults at the pin-level of hardware modules such as the processor, the bus, controllers, or other devices. The injection of faults is deterministic and can be reproduced if required. RIFLE can also detect particular states in which the faults do not harm the target system. The preeminent idea of RIFLE is to trigger and tracing methods adopted in digital logic analyzers with the logic demanded by the pin-level fault insertion. The tracing data is adopted for describing faults and their influence on the target system and for error propagation analysis [250].

- DEFINE

DEFINE is a distributed fault injection and monitoring environment to evaluate system dependability, analyze fault propagation, and validate fault-tolerant mechanisms. DEFINE can inject hardware faults (emulation) and software faults into a distributed system and observe their impact and propagation among mechanisms. It applies two fault injection methods: the first employs the hardware that interrupts to control fault injection and activation; the second adopts software traps to inject and monitor fault activation. DEFINE consists of four parts: a controller, a software monitor, a fault injector, and a workload generator. A target system is a group of connected machines. Therefore, DEFINE should be installed on a machine that is not part of the target system for not being affected by the faults [458].

- MEISTO-C

MEISTO-C [144] is an upgraded version of MEISTO (Multi-level Error/Fault Injection Simulation Tool) [192]. MEISTO-C uses a VHDL simulator for injecting faults via simulator commands that alter variables and signals defined in VHDL models. It grants users a set of predefined model faults, features to set up and control fault attacks. MEISTO-C supports estimating fault-tolerance mechanisms' coverage, investigating VHDL abstraction-level mappings, and validating fault-tolerant mechanisms.

- FERRARI

The Fault and ERror Automatic Real-time Injector (FERRARI) is a software fault injection tool that simulates transient errors and permanent hardware faults by corrupting the executing program's state. This is accomplished by using traps and system calls to enable software to emulate the effects of faults and errors. One of FERRARI's key features is to support the type, location, and time of fault and error injection. The fault injection mechanism is carried out by the concurrent execution of the target program and the fault injection mechanism process, which modifies the execution state of the target program. FERRARI comprises four modules: the initializer and activator, the user information, the fault and error injector, the collector and analyzer. The manager module controls these modules by coordinating the information flow and commands among the four modules [202].

- EXCEPTION

Xception is a fault injection platform for dependability analysis generates faults by software and monitors' activ to observe their impacts. EXCEPTION uses a set of debugging and performance monitoring features, such as performance counters and breakpoint registers - existing in processors - to inject faults by software. It supports a comprehensive collection of fault triggers as spatial, temporal, and data memory fault triggers. The target application is not modified, no software traps are inserted, and it is not required to execute the target application in special mode. The injected faults can be activated to emulate physical faults, even affecting the internal processor units. Xception consists of a kernel module, a fault setup module, and the Experiment Manager module (EMM). The kernel module consists of the exception handlers and the code for performing fault injection. The fault setup module is a library of functions whose only task is to receive the fault parameters from the host and pass them to the kernel. Fault setup is complicated by invoking the library function, StartXception(), from any processor in the target system. The target application or a detected process is executed if the application source code is not available. The EMM uses a distinct kernel for conducting fault injection experiments. The EMM runs on a host system and provides the user interface for fault definition, automatic fault experiment control, and collection of results. The target system is regarded as composed of the processor, system buses, and memory, where the processor is further divided into its functional units [69].

- FTape (Fault Tolerance and Performance Evaluator)

FTape generates software-implemented fault injection under stressful workload generation to increase the likelihood of errors spread to produce failures. FTAPE enables physical faults by software and monitors activity. For instance, a memory location can be flipped to emulate the impact of an alpha particle on a memory bit. The fault injector emulates faults on CPU registers, memory locations, and disks generates stressful workload to evaluate error propagation by monitoring workload activities. FTape supports defining the fault injection spot, instant, and workload threshold. Probability distributions may also be employed to specify the fault generation instant and location randomly. The tool comprises three main parts: the fault injector, the monitoring module, and a synthetic workload generator. The primary goal of the workload generator is to sustain a controllable workload that may disseminate erroneous states due to injected faults [440].
