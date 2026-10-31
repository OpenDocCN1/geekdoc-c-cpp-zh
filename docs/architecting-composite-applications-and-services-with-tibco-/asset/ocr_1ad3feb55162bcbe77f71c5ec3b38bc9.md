rule engine is executing building-block processes rather than individual activities, it makes it a bit easier for someone to understand the overall process than was the case with the rule service as process manager pattern discussed earlier.

There are many other options available for executing this type of business process. The design patterns given here are just illustrative examples showing the use of a rules service in this context. They are not intended to provide comprehensive coverage of the design alternatives.

# Rule Services and Data

Rules require information upon which to operate and, in turn, provide information to the rest of the business process reflecting the conclusions of the rules. The following sections describe two common design patterns for providing rules with access to information.

# Design Pattern: Rule Client Provides Data

A common means of providing data to the rule service is that the client invoking the service provides all the data required by the rules and receives the results of evaluating the rules as a data structure returned by the service (Figure 10-11).

This is an architecturally simple design for the rules service, since it is fully self-contained and only requires one interface. The down side is that the client has to assemble all of the required data and pass it to the rules service. If the data set is large, and especially if the data is largely repetitive from invocation to invocation, this may not be an optimal design from a performance perspective. You are trading performance for simplicity.

The simplicity of this design pattern, however, provides simplified design-time opportunities for defining rules. Rule engines that provide spreadsheet-like interfaces for rule definitions (including TIBCO BusinessEvents) generally follow this model, with one axis of the spreadsheet representing the elements of the input data and the other axis representing the elements of the result.

# Design Pattern: Rule Service Acquires Data

The other alternative is for the rule service to acquire some or all of the data required by the rules (Figure 10-12). In this design pattern the rule client typically provides some context information with each