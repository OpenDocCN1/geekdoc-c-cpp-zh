
## 9.23.2 Tools Supporting Simulation and Verification

To enable us to effectively Co-Simulate and Co-Verify our designs, we must have good tools at all levels of the process. Today there is a great variety of commercially available tools to help the embedded developer. Information on each of these can be found with the various vendors. Let us look at capabilities such tools have or should have.

### 9.23.2.1 Basic Capabilities

Most of such tools have a common set of basic capabilities. These include control of hardware and software simulation at all levels of the development process. Essential is support for initialization and breakpoint synchronization set in either the hardware or software domains. Encountering a breakpoint in either should support halting and potentially later resuming the system from the point where the system was halted. The ability to pass variables between hardware and software environments is also necessary. Finally, support for various levels of abstraction that includes high-level behavioral HDL or C/C++ models, detailed component structural level and hardware emulators that can range from complete software abstraction with hardware stubbed out and interface modeled to system in silicon.

### 9.23.2.2 Levels of Abstraction

Let us now examine the necessary abstraction levels supported by many tools in a bit more detail.

- Software only – Complete abstraction
The hardware is stubbed out and the interface is modeled or the application interfaces with stubbed out or modeled hardware through a device driver. Such an approach enables the functionality of the software to be tested and excludes detailed and constrained timing and asynchronous types of events.

- HDL simulation of hardware
The approach can include a functional model of system bus. Such a model can execute atomic (indivisible) bus cycles, include reads and writes to supporting arrayed logics with correct bus timings, and support modeling and handling asynchronous events such as interrupts. The method does not reflect the internals of the system CPU, missing registers, internal peripherals such as timers or signal converters but aids in debugging peripheral module functionality from the bus side when developing device drivers.

- Instruction Set Simulation (ISS) – Modeling the CPU
Modeling of the system CPU or digital signal processor is usually done as a C/C++ behavioral-level model. The simulation may run as a separate process under Unix/Linux. Such a process is separate from the HDL simulation sockets or similar inter-process communication scheme used to exchange information. The approach is not cycle accurate; however, an HDL wrapper surrounding the ISS model approach can be cycle accurate.

- CPU Emulator
With the CPU/DSP model extricated from the system and replaced by ICE module(s) for actual processor(s), it is possible to accurately replicate CPU bus cycle timing, thereby provide a robust platform for software development.

- Complete HDL Model
Supporting a complete HDL model gives a full HDL implementation of a complete system that can be executing at the register transfer level (RTL) or discrete device level. The approach tends to be more useful for developing the hardware rather than the software side. It is useful for verifying detailed and critical timing, hardware and software interactions, the boot process and memory interfaces and subsystems.

- **Hardware Emulation**
Under such an emulation, the hardware is modeled through some form of arrayed logic. Specifically this is an emulation; however, execution speed approaches that of a full ASIC. Contemporary arrayed logics can support the inclusion of CPU cores that will enable and facilitate both hardware and software debug.

## 9.24 OTHER CONSIDERATIONS

Several other factors must also be taken into consideration. The product must be able to be manufactured and tested. Such factors must be addressed early in the definition and design process. The three additional complementary and concurrent activities that need to be considered in today's business world are capitalization, reuse, and requirements and traceability management. Let us look briefly at capitalization; design reuse is one of the central threads in this text.

### 9.24.1 Capitalization and Reuse

#### 9.24.1.1 Capitalization

Capitalization is an essential element of the contemporary design process. Specifically, proper and efficient exploitation of intellectual properties (IPs) is very important today. Intellectual properties are designs, often patented, that can be sold or licensed to another party to develop and sell as (a part of) their product. The company MIPS, for example, designs computer architectures. It doesn't actually do any implementation itself; the design is its product; the ARM corporation does a similar thing.

#### 9.24.1.2 Reuse

Any consideration of component reuse is an activity that should be addressed and done during the functional and architectural design phases of the development process. Such activities can be considered sometimes during prototyping as well. The end purpose is to help designers shorten development cycles.

Component reuse is facilitated in two ways: present and future.

- **Present**
By identifying external (existing) functional or architectural components that can satisfy some portions of the current system's desired functionality.

- **Future**
By identifying components of the solution under design that can or will be reusable on other or future projects or products.

To be reused, a component needs to be:

- Well defined
- Properly modularized
- In conformance to some interchange standard.

A well thought out, well designed module will be much easier to adapt to a new situation than one that someone pieced together for some ad hoc purpose and barely got working. The same is true for a portion of a well-modularized system. If, during the design phase, one makes decisions with an eye to modules that could be reused, the chances of such reuse are greatly enhanced. Finally, if the goal is for a module to have wider applicability than a local venue, then the designs must accommodate existing national and international standards. With today's international market growing daily, it is incumbent upon us to design to such standards. Once again, the real-world intrudes and trade-offs are part of the process. When designing for reusability or striving for a modular design, other factors need to be considered. If there is not enough ROM space for the code if it is designed to be completely modular, the design may be modified to be very application specific. While the decision might create problems in the future, we will end up with a noncompetitive product if the budget is exceeded.

### 9.24.2 Requirements Traceability and Management

#### 9.24.2.1 Requirements Traceability

Requirements traceability refers to the ability to follow the life of a requirement (from the original specification) in both the forward and reverse directions through the entire design process and the design. Traceability is potentially a one-to-many relationship between a requirement and the components it relates or traces to (or that implement it).

An accurate and complete record of traceability between requirements and system components provides several important pieces of information through the product life cycle. Among these are:

- The means for the project manager and (potentially) the customer to monitor the development progress.
- A path that can be used during the verification and validation of the product against the original specification. Knowing where and how a specified requirement has been implemented facilitates confirming that the requirement has been faithfully implemented.
- A means of identifying which hardware or software modules are affected if a requirement changes.

#### 9.24.2.2 Requirements Management

- Requirements management addresses.
- Requirement modifications.
- Changes.
- Improvements.
- Corrections.

During the design, such changes are difficult to avoid for many reasons. Therefore, a clear procedure that facilitates a way to accommodate and track such modifications has to be used during the complete design process.
