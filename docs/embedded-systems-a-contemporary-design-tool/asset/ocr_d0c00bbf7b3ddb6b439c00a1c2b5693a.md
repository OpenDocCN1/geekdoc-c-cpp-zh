defining the software implementation or block diagram (using any of a variety of methods) for each software component of the architecture.

Each functional subset to be implemented in software is described by a detailed software specification that expresses the priority of each task and the spatial (data coupling), and temporal dependence relations between tasks. UML diagrams, including detailed state charts, timing diagrams, sequence diagrams, activity diagrams, and collaboration diagrams, can all be very useful at this stage in the design.

A software implementation may or may not use a real-time kernel. With an off-the-shelf real-time kernel, the development time is reduced, but not the factory cost or time-based performance specifications. For systems that do not use a real-time kernel (which represent 80–90% of small and medium systems) one can achieve a better optimization of the design when addressing high-speed hard real-time constraints. Under such circumstances, the solution is being hand tailored to the specific problem rather than adapting a general purpose solution to a specific case.

For the software design, the following must be analyzed and decided:

+   - Whether to use a real-time kernel or not.
+   - Can several functions be combined in order to reduce the number of software tasks? If so, how?
+   - A priority for each task.
+   - An implementation technique for each intertask relationship.

# Rate Monotonic Scheduling

When it is appropriate, a real-time kernel or the services of an operating system can be used. In general, the main objective is to reduce the complexity of the organizational part in order to reduce the size and complexity of the software and the resulting development, testing, and debugging times.

Under such circumstances, a frequent choice is the Rate Monotonic Scheduling policy (this will be discussed in Chapter 12; more frequently executed tasks are assigned a higher priorities). Permanent functions (those that run continuously without an activating event) and some cyclic functions without timing constraints are usually implemented within a background task.

For the implementation of intertask relationships, it is desirable to use procedure calls as much as possible, thereby simplifying the organizational part and reducing the inter-task overhead. Such an implementation is only possible between functions with increasing relative priorities. Tasks triggered by hardware events are invoked through the processor interrupt or polling subsystems.

For each specific subpart of the system in which the partition is not obvious, a detailed specification is written; the final hardware/software partition is determined through a process of successive refinements as was done in the earlier decomposition process. Each hardware/software partition must also identify and include the hardware interfaces and the software drivers to support any inter-component communication.

The result is a complete mapping of all remaining functions and functional relations onto the hardware architecture. Among the important criteria that we strive to optimize are:

+   - Implementation (or factory) cost.
+   - Development time and cost.
+   - Performance and dependability constraints.
+   - Power consumption.
+   - Size.