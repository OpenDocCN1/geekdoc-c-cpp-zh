
## 9.16.2 Coupling

Coupling is a heuristic that provides an estimate of how interdependent the modules are. Tightly coupled modules will generally utilize shared data or interchange control information. As module interdependence increases, so does the complexity of managing those modules and the more difficulty one will have in:

- Debugging the design during development.
- Troubleshooting the system in the event of field failures.
- Maintaining the modules and system.
- Modifying the design to add features or capabilities.
- Ensuring a secure system.

The major goal is to make the system's modules as independent as possible and to reduce or minimize coupling.

**Design Heuristic.** The lower the coupling, the better job that has been done during partitioning.

During the early stages of the design, think about the following to help to reduce coupling:

- 1. Eliminate all unessential interaction between modules.
  If a particular piece of functionality or shared parameter is not part of the intended task of two modules, then eliminate it.

- 2. Minimize the amount of essential interaction between modules.
  While this sounds the same as the previous point, it is not. If an early analysis establishes that some interaction with another module is necessary, effort should be made to reduce the complexity of that required interface. The goal is to keep things simple.

- 3. Loosen the essential interaction between modules, if possible. Unless the environment demands a high degree of coordination between several modules to accomplish a task or to ensure error free communication, simply pass the module the information necessary to get the job done. Thereafter, wait for an indication that the task has completed. Execute some other part of the task.

Some of the ways to help to reduce complexity include:

- a. Reduce the number of interconnections between modules and thereby, reduce the number of pieces of data that must flow between modules.

- b. Try to take the most direct route to a signal or piece of data as appropriate.
  In some cases the best implementation is to use a proxy as an interface to a signal or piece of data. In general, however, it is best to reduce the number of modules involved.

- c. In general, avoid using shared global variables. A better method is to pass data into a module via its parameter list or calling interface. With embedded applications, however, at times such sharing is critical to meeting time constraints. For security reasons, however, such sharing should be constrained and controlled.

- d. Avoid arcane interconnections between or among modules. A guiding principle underlying all design is to keep things simple.

- e. Don't hard code values into a module's parameter list or calling interface unless absolutely necessary. We must do so on occasion when an interface module or port must be at a specific address location; do not make this a general practice.

## 9.16.3 Cohesion

**coupling, cohesion** An idea related to *coupling* is *cohesion*. The notion of coupling addresses the partitioning of a system; cohesion addresses bringing the pieces together. Cohesion is a measure of strength of the functional relatedness of elements in a module. The goal is to create strong, highly cohesive modules whose elements are genuinely and tightly related to one another. Conversely, elements should not be strongly related to elements in another module. We want to maximize cohesion and minimize coupling.

**maximize, minimize** The use of cohesion as a reliability and quality metric has been around since the mid-1960s. A number of years of refinement and integration of the ideas of many people studying various designs and design approaches led Constantine and Yourdon, *Structured Design* (Prentice-Hall, 1979), to formulate a cohesion scale based on an ease of maintenance metric. Let's look at several different kinds of cohesion.

- **Functional cohesion.** The module implements a single task, and all comprising elements contribute to the execution of that one task.
- **Sequential cohesion.** The module implements a task as a sequential set of procedures. The output data of each procedure becomes the input data to the next. All of the comprising elements are involved in one of those procedures.
- **Communicational cohesion.** The module implements a task that has a number of procedures working on the same set of input data such as an image processing task.
- **Procedural cohesion.** The module implements a number of procedures that may or may not be related to a common activity. Control, rather than data, flows from one procedure to the next.
- **Temporal cohesion.** The module implements a number of unrelated procedures or activities that are sequentially ordered in time.
- **Logical cohesion.** The module implements a number of procedures that are possible alternative methods for accomplishing a task. A subset of those alternatives is selected by an outside user to actually execute the task.
- **Coincidental cohesion.** The module aggregates a number of unrelated procedures. Such cohesion, or lack thereof, should not be used.

We compare the different kinds of cohesion and coupling from several different perspectives in Table 9.1. The ranking is Excellent/Easy = 5 ... Poor/Difficult = 1.

## Table 9.1 Comparison of Coupling and Types of Cohesion from Different Perspectives.

| Cohesion | Coupling | Ease of modification | Ease of understanding | Ease of maintenance |
|---|---|---|---|---|
| Functional | 5 | 5 | 5 | 5 |
| Sequential | 4 | 4 | 4 | 3–4 |
| Communicational | 3 | 3 | 3 | 3 |
| Procedural | 2–3 | 2–3 | 2–3 | 2 |
| Temporal | 1 | 3 | 3 | 2 |
| Logical | 1 | 1 | 2 | 1 |
| Coincidental | 1 | 1 | 1 | 1 |

Cohesion and coupling analyses provide a good set of metrics by which to begin to assess the high-level architectural aspects of a design. Remember, however, that both are guidelines. The work to ensure that the design is solid and that it is thoroughly tested still needs to be done.

There are plenty of good designs that require tightly coupled modules; CDMA cell phones are a good example. One can have tightly coupled multiprocessor designs as well as designs based on message passing. The implication is not that one design is right or wrong, or better than the other; it is just how it was done to meet the requirements.

## 9.16.4 A Few More Considerations

**spatial** With today's systems, a spatial point of view is often essential. This is an external view of the system and it yields a distributed functional architecture. With such a view, performance and communication costs are taken into consideration. Closely associated with the spatial viewpoint is that of resource allocation; again, this is an external view. Such efforts result in a “resource architecture.” Once again, performance, costs, and dependability are factors that must be considered.

**hardware** Finally, one must consider the hardware and the software. Decomposition becomes a design process that leads to a hardware architecture as was discussed earlier. Now performance must be considered. As embedded developers, we are playing a direct role in the design and selection of the hardware platform as well as the software environment. Making trade-offs intelligently in these two areas can take us a long way toward developing a safe, robust, and high-quality/high-performance system.

## 9.16.5 Approaches to Partitioning and Mapping

As we take this next step in the design process flow, our objective is to allocate operations comprising system behavior to the hardware and/or the software. There are a variety of different methods by which to attack the partitioning problem. We recognize that there are two extremes: a software-oriented model and a hardware-oriented model. The former initially puts everything into software while moving time critical pieces of functionality to hardware as necessary to meet time or speed constraints. The latter initially puts everything into hardware while moving non-time critical pieces of functionality to software as appropriate to meet cost constraints. That said, let us begin by codifying the various approaches according to main properties or characteristics.

### 9.16.5.1 The Approach

- The model. Typically the system is expressed as a graph (from graph theory) derived from an abstraction of the system design specification.
- Cost function. One metric for assessing a partition is to ask the question: How does such a partition negatively impact system performance? The question suggests devising a partition cost function that guides the partitioning algorithm toward minimizing the value of the function. In theory, the best partition is one that yields a minimum value.

Such a function should measure the consequences of hardware/software allocation bounded by two extremes: all hardware and all software and the effects on system timing behavior, power consumption, and memory loading.

Partitioning in software analyzes the statistical behavior of the executing program to drive the algorithm. Partitioning in hardware is looking at static allocation of functionality.

- Granularity. Is usually based upon elements of the specification language: processes, tasks, loops, etc.

Let's now delve down and examine some methods that can be utilized to execute an approach.

### 9.16.5.2 The Method

At this stage in the process of developing a system architecture, our goal is to map the functional blocks that we have identified to hardware, software, or both. How is the partitioning executed? What is the algorithm?

Possible alternatives include aggregating or grouping elements, iteration, mathematical relations, or greedy heuristics that build the solution sequentially then picks the "best" local decision without consideration for consequences. Here, with the various alternatives, best is subjective based upon the application and the designer(s).

We will now look at several different partitioning methods.

### 9.16.5.2.1 METHOD 1 DUE TO KUMAR

We can view the system being designed as comprising the following abstract sets:

- Set of hardware resources.
- Set of available software functions.
- Set of communications and control between the hardware and software units.
- Set of functions to be implemented. Such functions, determined by an earlier functional decomposition of the system, will be assigned to the hardware, software, or communications.

Formally, as we see expressed in Eq. (9.1) and modeled Figure 9.32, we have a mapping, F, from the set comprising our starting functional blocks to the physical hardware, software, and communications blocks.

```
F: functional blocks → hw, sw, comms
```
