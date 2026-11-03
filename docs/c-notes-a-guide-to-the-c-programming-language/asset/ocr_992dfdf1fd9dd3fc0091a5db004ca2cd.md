same state as obtained at entry to the function. Moreover, the mode bits of the FPP must be double and int as described in [7.0]. Returned values are expected as follows, depending on the type:

| Type | Register |
|---|---|
| char, int, short int, unsigned int, pointer | R0 |
| long int | R0/R1 |
| floating, double | FR0 |

In machines that do not have a FPP, floats could be returned in R0/R1, and double results in a globally declared accumulator c.fe. The c.fe would behave exactly as FR0; i.e., it is assumed to be volatile in function calls and must be saved, along with other registers, to make code reentrant. There also would be a c.fe analogous to FR1, but there might not be any that is allocatable and that corresponds to FR2 and FR3.

The condition codes are not assumed to be meaningful on return from any C function.

In most implementations, the compiler meticulously maintains a chain of stack frames, so that at any time

+   1) FP is the current frame pointer
+   2) 2(FP) is the return address from the most recent call
+   3) 0(FP) is the previous frame pointer

An exception to this would be any function compiled for the 11/40, LSI-11 floating point option. In this case, a possible implementation would be as follows:

+   1) FP is the current frame pointer
+   2) 6(FP) is the return address from the most recent call
+   3) 4(FP) is the previous frame pointer
+   4) 0(FP) is one floating accumulator
+   5) -4(FP) is the other floating accumulator