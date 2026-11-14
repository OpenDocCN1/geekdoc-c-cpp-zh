# 14.13.2.1.1 SYSTEM-LEVEL MODEL

The system-level model is described by a hierarchical structural model and is represented by a set of communicating functions or processes. Typically, the functions are specified using a behavioral model.

# 14.13.2.1.2 FUNCTIONAL MODEL

A functional model expresses the system under design as a collection of functions. Its structure is hierarchical and graphical, and describes a system by a set of interacting functional elements. The behavior of each element is independent of any future hardware or software implementation.

# 14.13.2.1.3 PHYSICAL MODEL

The physical model describes the architectural structure of the system based on real components and their interactions.

# 14.13.2.1.4 STRUCTURAL MODEL

A structural model specifies the organization of the system based on the components in the system and the interconnections among those components. The model includes both functional and physical-level elements as well as the mapping between them. The model binds the functional to the physical views and can be used at any level of abstraction.

# 14.13.2.1.5 BEHAVIORAL MODEL

There are a wide variety of models in this category. As noted earlier, such a model is usually based on symbols to represent qualitative aspects, and behavior is frequently expressed as a function of time.

# 14.13.2.1.6 DATA MODEL

A data model or entity-relation model represents the world in terms of entities and their attributes and the relations between/among those entities.

# 14.13.3 Timers

Timers can be associated with various busses or pieces of code in the system. One can then start the timer when entering the block of code to be timed and stop the timer on exit. Such an approach is best for timing blocks of code. The approach is not particularly effective for a long program.

# 14.13.4 Instrumentation

Another effective way of assessing the performance of a system is simply to measure it. Numerous instruments, such as the basic logic analyzer and code analyzer, permit a system to be instrumented and its performance to be assessed qualitatively. Such instruments can measure maximum and minimum times, time loops, identify nonexecuted code, and capture rates of execution, among other things. Such instruments can also identify the most frequently used code so that it may be optimized in the future. The major caveat with any such measurements is that they are only as good as the input to the system. If you are not executing both typical and boundary condition applications, the quality of any measurements