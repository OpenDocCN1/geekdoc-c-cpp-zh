# 9.11.2.1 Characterizing the System

Characterization of the system begins with identifying inputs and outputs.

# 9.11.2.1.1 SYSTEM INPUTS AND OUTPUTS

The system interacts with the real world through the entities described and defined in the environmental characterization. The inputs to the system are the outputs from environmental entities and the outputs from the system are the inputs to the environmental entities. One can easily see that the system I/O has already been characterized in environmental entity specification.

For each such I/O variable, the following information is already available:

+   - The name of the signal.
+   - The use of the signal as an input or output.
+   - The nature of the signal as an event, data, state variable, and so on.

Working with the environment specification, one can write the structure, domain of validity, and physical characteristics of each signal. To these, one can add any technical or technological constraints that are identified.

# 9.11.2.2 FUNCTIONAL VIEW

As was done with the specification of the environment, focus now turns to the function that the system is intended to perform. Before it is designed, the system appears as a black box. It can only be viewed from an external point of view. A section on functional behavior is now included in the specification.

The functional description defines the external behavior of the system. It characterizes the effects of the system outputs on the environmental entities and the system's intended response to inputs from the environmental entities. It elaborates on how the system is used and to be used by the user. Such a specification is equivalent to developing a model of the system.

The functional description can be captured in a variety of ways. One effective approach is to use the UML tools discussed earlier. One can construct one such view through use case and class diagrams. Another view can be gained through high-level state charts and activity diagrams; data and control flow diagrams commonly used in structured design methodologies give a third view.

As one formulates these diagrams and the specification, care must be taken to ensure that:

+   - The specified (and ultimately modeled) states are appropriate to the application.
+   - The actions associated with system I/O that are captured in the specification are necessary to express functional specification and accurately reflect the desired (external) behavior of the system as perceived and intended by the customer.
+   - The conditions or constraints on its behavior are only a function of the system inputs, the specified states, the internal events, and the appropriate time demarcation (relative or absolute).
+   - The possible exceptions associated with each of the use cases.