# Embedded C Coding Standard

# 6.5 Interrupt Service Routines

Rules:

+   a. Interrupt service routines (ISRs) are not ordinary functions. The compiler must be informed that the function is an ISR by way of a #pragma or compiler-specific keyword, such as `__interrupt`.

+   b. All functions that implement ISRs shall be given names ending with `_isr`.

+   c. To ensure that ISRs are not inadvertently called from other parts of the software (they may corrupt the CPU and call stack if this happens), each ISR function shall be declared static and/or be located at the end of the associated driver module as permitted by the target platform.

+   d. A stub or default ISR shall be installed in the vector table at the location of all unexpected or otherwise unhandled interrupt sources. Each such stub could attempt to disable interrupts of the same type, say at the interrupt controller, and assert().

![](bbox=[0.789, 0.283, 0.856, 0.345])