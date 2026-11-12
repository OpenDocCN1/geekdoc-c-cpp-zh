| Technical Specifications | 3.0 | 3.2 | 3.5 | 3.7 | 5.0 | 5.2 | 5.3 | 6.0 | 6.1 | 6.2 | 7.0 | 7.5 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| reference bound to a CUDA array | | | | | | | | | | | | |
| Maximum width (and height) for a cubemap surface reference bound to a CUDA array | \multicolumn{12}{c}{32768} |
| Maximum width (and height) and number of layers for a cubemap layered surface reference | \multicolumn{12}{c}{32768 x 2046} |
| Maximum number of surfaces that can be bound to a kernel | \multicolumn{12}{c}{16} |
| Maximum number of instructions per kernel | \multicolumn{12}{c}{512 million} |

# H.2. Floating-Point Standard

All compute devices follow the IEEE 754-2008 standard for binary floating-point arithmetic with the following deviations:

+   - There is no dynamically configurable rounding mode; however, most of the operations support multiple IEEE rounding modes, exposed via device intrinsics;

+   - There is no mechanism for detecting that a floating-point exception has occurred and all operations behave as if the IEEE-754 exceptions are always masked, and deliver the masked response as defined by IEEE-754 if there is an exceptional event; for the same reason, while SNaN encodings are supported, they are not signaling and are handled as quiet;

+   - The result of a single-precision floating-point operation involving one or more input NaNs is the quiet NaN of bit pattern 0x7fffffff;

+   - Double-precision floating-point absolute value and negation are not compliant with IEEE-754 with respect to NaNs; these are passed through unchanged;

Code must be compiled with `-ftz=false`, `-prec-div=true`, and `-prec-sqrt=true` to ensure IEEE compliance (this is the default setting; see the `nvcc` user manual for description of these compilation flags).

Regardless of the setting of the compiler flag `-ftz`,

+   - Atomic single-precision floating-point adds on global memory always operate in flush-to-zero mode, i.e., behave equivalent to `FADD .F32 .FTZ .RN`,

+   - Atomic single-precision floating-point adds on shared memory always operate with denormal support, i.e., behave equivalent to `FADD .F32 .RN`.

In accordance to the IEEE-754R standard, if one of the input parameters to `fminf()`, `fmin()`, `fmaxf()`, or `fmax()` is NaN, but not the other, the result is the non-NaN parameter.