Let us examine the co-simulation block first the synthesis block. If we examine the flow, we cannot afford to build a hardware platform for each iteration as we try out the design, make adjustments, and try again. It is simply too expensive and takes too much time. We want to be able to iterate through the process a number of times, refining the design with each iteration. The desideratum during the early stages of design is that we want maximum flexibility. During the later stages of a design, we would like to be able to introduce physical hardware including the processors, FPGAs, and ASICs. Of these, the ASICs would be the most difficult since take most time to build. Certainly, we could have processors and FPGAs earlier.

To satisfy our objectives during early stages, we use simulated hardware running real software. Later we migrate toward real hardware. Our goal is to be able to execute the software as fast as possible and we want to keep both simulations synchronized to ensure proper performance in the ultimate target platform.

To accomplish such a goal, one could simulate the target hardware design running on a general purpose HDL based simulator then execute the software solution on such a simulation or on a host that is faster than the target platform. For larger systems, such an approach becomes quickly impractical.

# 9.22.1 Tools Supporting Modeling

Co-Design tools enable today's designers to work at a high level of abstraction as well as at the detailed level to enable them to gain a high level of confidence that when the system is ultimately fabricated it will perform according to initial specifications. Our typical simulation platform comprises the computer and the hardware and software each modeled as a process. Hybrid environments add co-processors to assume part of the computational load. The remainder remains in software.

We distinguish between simulation and emulation. With simulation, we model the software and hardware and we make best effort to duplicate the real system. With emulation, we augment with hardware, as necessary, to ensure that we meet all timing requirements.

Emulation is termed to be cycle accurate. This is usually done with FPGAs or some similar device. Emulation becomes essential when trying to identify higher speed, time critical operations. If we are designing a system to operate in the GHz region, we are not going to do that with a software simulation. Under such a circumstance, we are using a hybrid or extensible simulation. Emulator based or driven simulators have difficulty with behavioral based models.

# 9.22.2 Types of Simulations

+   - Gate level
+   - Cycle based
+   - Event driven
+   - Data flow

We identify several major types of simulation: gate level, cycle based, event driven, and data flow. We may use several different simulators or simulation methods during the course of design. It is important to always choose the best tool for the job.

+   **Gate Level Simulations**
+   Gate level simulations try to replicate, as much as possible, the gate level implementation behavior of the CPU. The method is highly inefficient and impractical for larger systems.

+   **Cycle-Based Simulations**
+   Cycle-based simulations simulate the bus interface and associated timing. The program is executed on a high-level instruction set interpreter. Signal state is