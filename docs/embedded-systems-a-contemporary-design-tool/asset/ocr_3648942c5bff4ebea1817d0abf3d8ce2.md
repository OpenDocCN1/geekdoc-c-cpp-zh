Traffic flows in one direction on the outer ring and in the opposite direction on the inner ring. On failure, the loss of a single link on either ring still leaves one of the rings intact, as we see in the center drawing, which shows two alternate failures. If both links are severed between any adjacent nodes, as in the right-hand drawing, a single ring remains intact.

# 8.14 DATA AND CONTROL FAULTS – DATA BOUNDARY VALUES

One of the essential steps during the early phases of a design is the definition of the interface signals among the system functions and then the modules. This process involves specifying the type and range of each signal. As each of those decisions is made, one must further consider how the system will behave/respond if the input data either does not match the expected type or exceeds the specified range. In addition to deciding what to do if the signal exceeds the specified range, one must also consider the proper course of action if (and when) the signal returns to the proper values.

The problem can be addressed from both the design and operational sides. During design, one must ensure that the input data is in bounds prior to incorporating it in any calculations or before making any irrevocable decisions. Furthermore, one must decide how to treat out-of-bounds values at runtime.

Under no circumstances should an out-of-bounds piece of input data ever be mapped, without warning, into one that is in bounds. That said, boundary tests must be incorporated into the runtime code to confirm that input data has values (and types) that are within the specified upper and lower bounds. Furthermore, one needs to decide what to do if such bounds are exceeded. Alternatives include:

+   - Hold at max or min value
+   - Alarm
+   - Combination.

# 8.14.1 Type Conformance

The task of ensuring type conformance for input signals is somewhat easier in an embedded application because we have greater control over inputs and their characteristics than one might find in the typical desktop application. Runtime type mismatch should not be a major issue. We will discuss such issues in greater detail when we address security issues.

When new features are added to a legacy design, one must be sure that existing functions are invoked with the proper signature. Extra care must be taken when the application is written in a language such as C++ that supports overloaded functions.

# 8.14.2 Boundary Values

Figure 8.16 illustrates a typical signal and a specified range or limits on that signal. At points A and B, the signal is at the low and high boundaries, respectively; at these two points, the signal value remains in range.

At C1, the signal exceeds the specified range in the negative direction and continues decreasing. It reaches a negative peak and begins increasing, crossing the lower bound at C2. The increase continues until the upper bound is crossed at D1. The behavior at the lower bound is repeated at the upper bound, and eventually the signal crosses back into the specified range at D2.