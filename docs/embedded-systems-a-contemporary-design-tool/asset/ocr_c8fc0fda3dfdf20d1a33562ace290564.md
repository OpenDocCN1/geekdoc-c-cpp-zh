# 9.12.1 The System

As part of formalizing and quantifying the system’s requirements, one must attach concrete numbers, tolerances, and constraints to all of the system’s input and output signals. All timing relationships must be defined. The system’s functional and operational behaviors are described in detail.

# 9.12.2 Quantifying the System

The quantification of the system’s characteristics begins with the inputs and outputs, based on the specified requirements. The necessary technical details are added to enable the engineer to accurately and faithfully execute the actual design.

+   System Inputs and Outputs

For each I/O variable, the following are specified:

+   The name of the signal.

+   The use of the signal as an input or output.

+   The nature of the signal as an event, data, state variable, and so on.

Starting with the requirements specification, we provide detailed descriptions as necessary and incorporate any additional technical or technological constraints that may be needed.

+   The complete specification of the signal, including nominal value, range, level tolerances, timing, and timing tolerances.

+   The interrelationships with other signals, including any constraints on those relationships.

+   Responsibilities – Activities

+   Functional and Operational Specifications

The functional and operational specifications that will quantify the dynamic behavior of the system are now formulated. The functional requirements specification identifies the major functions that the system must perform from a high-level view. The operational specification endeavors to capture specific details of how those functions behave within the context of the operating environment.

The manner in which a particular function must operate, the conditions imposed on the operation, and the range of that operation are now captured. The specification must consider concrete numbers - precisions and tolerances.

Precisions Tolerances

All variables in the functional specification, all operating conditions, and all ordinary and extraordinary operating modes must be quantified. The specification may include domain-specific knowledge that is proprietary or heuristically known to the customer. Such knowledge can be very important to the design.

In stating the specific design requirements for the system, one can use tables, equations, or algorithms, formal design language, or pseudocode, flow diagrams, or detailed UML diagrams such as state charts, sequence diagrams, and time lines. Schematics, codes, or parts lists are not included, except in limited circumstances.

+   Technological (and Other) Specifications

The technological portion includes all detailed and concrete specifications that are relevant to the design of the system hardware and software. Five areas that should be considered can easily be identified.