# Performance, Reliability, and Availability Evaluation of Computational Systems

These leading platforms provide the grounds for more recent tools. Besides, the section also highlights a few recent appliances. Nevertheless, it does not intend to offer a comprehensive overview of present-day tools at hand; instead, it only offers relevant initiatives in the field.

+   - Czeck, Segall, and Siewibrek

Czeck, Segall, and Siewibre proposed a software fault insertion for embedding transient faults in the processor data path, control path, memory system, and transmission bus. The motivation for implementing such a tool was to reduce the complexity of hardware fault insertion and the respective automation processes. Besides, software inserted faults are repeatable within a system and across architectural and implementation boundaries. This tool supports defining the location, timing, and duration of the inserted faults [89].

+   - FIAT

The Fault-Injection-based Testing environment (FIAT) is an automated real-time distributed accelerated fault injection environment implemented to emulate hardware and software faults to support validation and uncover deficiencies in systems' error detection mechanisms, recovery procedures to guide tradeoffs between alternative designs. Faults are introduced by a fault injection library linked with the target process for corrupting memory requests from an external program. A library code is also employed to watch the process behavior and for data gathering. A solution intends to subdue the operating system's security mechanisms that prevent external processes from altering the state of a target process. FIAT also provides a user interface and a hardware/software structure for aiding the definition of workloads, faults, with means for defining fault classes, choosing where, when, and how long errors will strike, and how they will communicate with executing code or data. FIAT provides the analyst with means... for data analysis. One of the significant flaws of FIAT was linking the fault injection library at compilation time using the object or source code of the target. This procedure is unsuitable for third-party software [374, 375].

+   - FOCUS

FOCUS is a design automation platform for analyzing jet-engine controllers that employ a simulation environment based on SPLICE for tracking the impact of transient faults. The simulation environment feeds the analysis software with faults to discover critical design features that may lead to system failures and enable the identification of fault propagation paths and the most sensitive modules to fault propagation [75].

+   - MESSALINE

MESSALINE is a pin-level fault injection platform composed of four modules: the injection module, the activation module, the collection module, and the management module. The activation module assures the correct initialization of the target system.