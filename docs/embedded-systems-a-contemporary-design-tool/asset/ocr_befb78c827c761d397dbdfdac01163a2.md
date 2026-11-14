The operation of the CFSM comprises four phases:

+   1. Idle.
+   2. Detect an input event.
+   3. Execute a transition according to which events are present and match the associated transition relation.
+   4. Emit an output event.

Consequently, a state transition triggered by an input signal is reflected sometime later in an output change.

A timed trace of events is an ordered sequence in time. Time is monotonically non-decreasing. No two events with same name can occur simultaneously. This implies that no communication channel can carry two values at the same time, for example, two instances of the same interrupt.

The globally asynchronous nature of the CFSM facilitates partitioning the system model into hardware and software components. The low-level structure of individual CFSMs makes the synthesis of hardware or software rather straightforward.

# 9.19.5.8.1 LIMITATIONS

The communication mechanism is very specific. It does not easily support complex data types or data transformations. It can model other schemes such as blocking messages and shared variables; it can be cumbersome, however. Similar to the EFSM, it is too low level to easily support specification. Generally, formal specification languages more effective.

# 9.19.5.9 Program State Machines

The program state machine extends the FSM by integrating a hierarchical concurrent FSM and programming language concepts. The model is similar to the RAM MOC. In the machine, the concept of state represents a distinct mode of computation. Only a subset of program states can be active at any one time carrying out an associated computation or operation.

A program state can be compound, i.e. made up of a set of program states, or elementary, in which it comprises a single program state. Compound states may be executing in sequence or in parallel, similar to the UML State Chart and, thus, useful for modeling multitasking operation. Elementary states are modeled as a sequential algorithm in an imperative language. Assignments are the only statements in such a language responsible for a change in state.

Transitions between sequential program states are of two types:

+   - Transition Immediate arcs, in which the transition occurs as soon as a condition becomes true, independent of the state of subprogram states: active – inactive or computation complete – not complete. Such arcs are intended to address reset or exception conditions such as interrupts.
+   - Transition on completion arcs, in which the transition occurs when the state has finished an activity. Such behavior is similar to signal-wait and signal-continue semantics in semaphores and monitors and are loosely analogous to guard conditions in UML state charts.