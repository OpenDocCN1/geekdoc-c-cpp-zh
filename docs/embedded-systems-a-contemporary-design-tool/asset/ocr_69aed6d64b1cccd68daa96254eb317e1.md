# 9.23.2 Tools Supporting Simulation and Verification

To enable us to effectively Co-Simulate and Co-Verify our designs, we must have good tools at all levels of the process. Today there is a great variety of commercially available tools to help the embedded developer. Information on each of these can be found with the various vendors. Let us look at capabilities such tools have or should have.

# 9.23.2.1 Basic Capabilities

Most of such tools have a common set of basic capabilities. These include control of hardware and software simulation at all levels of the development process. Essential is support for initialization and breakpoint synchronization set in either the hardware or software domains. Encountering a breakpoint in either should support halting and potentially later resuming the system from the point where the system was halted. The ability to pass variables between hardware and software environments is also necessary. Finally, support for various levels of abstraction that includes high-level behavioral HDL or C/C++ models, detailed component structural level and hardware emulators that can range from complete software abstraction with hardware stubbed out and interface modeled to system in silicon.

# 9.23.2.2 Levels of Abstraction

Let us now examine the necessary abstraction levels supported by many tools in a bit more detail.

+   • Software only – Complete abstraction
+   The hardware is stubbed out and the interface is modeled or the application interfaces with stubbed out or modeled hardware through a device driver. Such an approach enables the functionality of the software to be tested and excludes detailed and constrained timing and asynchronous types of events.

+   • HDL simulation of hardware
+   The approach can include a functional model of system bus. Such a model can execute atomic (indivisible) bus cycles, include reads and writes to supporting arrayed logics with correct bus timings, and support modeling and handling asynchronous events such as interrupts. The method does not reflect the internals of the system CPU, missing registers, internal peripherals such as timers or signal converters but aids in debugging peripheral module functionality from the bus side when developing device drivers.

+   • Instruction Set Simulation (ISS) – Modeling the CPU
+   Modeling of the system CPU or digital signal processor is usually done as a C/C++ behavioral-level model. The simulation may run as a separate process under Unix/Linux. Such a process is separate from the HDL simulation sockets or similar inter-process communication scheme used to exchange information. The approach is not cycle accurate; however, an HDL wrapper surrounding the ISS model approach can be cycle accurate.

+   • CPU Emulator
+   With the CPU/DSP model extricated from the system and replaced by ICE module(s) for actual processor(s), it is possible to accurately replicate CPU bus cycle timing, thereby provide a robust platform for software development.

+   • Complete HDL Model
+   Supporting a complete HDL model gives a full HDL implementation of a complete system that can be executing at the register transfer level (RTL) or discrete device