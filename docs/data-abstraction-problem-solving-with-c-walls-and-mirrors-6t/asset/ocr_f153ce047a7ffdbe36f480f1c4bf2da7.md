+   The RUP organizes development into four phases:
+   * Inception—feasibility study, project vision, rough estimates of time and cost
+   * Elaboration—refined project vision, iterative development of core system, development of system requirements, more accurate time and cost estimates
+   * Construction—iterative development of remaining system
+   * Transition—testing and deployment of the system

We will look at the characteristics of each phase. Figure D-2 shows how the RUP development phases relate to iterations.

# FIGURE D-2 RUP development phases

![](bbox=[0.15, 0.29, 0.68, 0.46])

# D.2.1 Inception Phase

During the inception phase, we define the scope of the project and decide whether the project is feasible. If a team has already implemented solutions for similar problems, and the solution is clearly feasible, the inception phase may be very brief.

At a minimum, the inception phase must define an initial set of system requirements and choose the length of the iteration timebox. While defining the initial requirements, you generate a core set of use case scenarios and determine which elements of the solution involve the greatest risk. This set of scenarios and the highest-risk aspects of the solution are the focus of the first iterations in the elaboration phase. Note that the inception phase is not an iteration. You should not try to develop all—or even most—of the use case scenarios during inception. Usually only about 10 percent of the use case scenarios are written in any detail during the inception phase.

> The inception phase defines a project's scope and feasibility
> 
> The elaboration phase develops a core system and addresses high-risk elements

# D.2.2 Elaboration Phase

During the elaboration phase, the system's core architecture is iteratively developed, high-risk elements of the system are addressed, and most of the system requirements are defined. The core architecture is composed of those software components that are central to the system. For example, the objects represented in the Unified Modeling Language (UML) class diagram in Figure C-4 of Appendix C would make up the core architecture of that banking system.

The elaboration phase extends over two or more iterations. If the elaboration phase has only one iteration, no feedback can come into play. Multiple iterations are necessary when developing the correct solution incrementally and adaptively.

The usual reason for a solution to fail is that high-risk elements were not handled adequately. Early in the elaboration phase, high-risk elements need to be addressed and resolved. If these