# ISO/IEC 9899:2011 (E)

math_errhandling & MATH_ERRNO is nonzero, the integer expression errno acquires the value ERANGE; if the integer expression math_errhandling & MATH_ERREXCEPT is nonzero, the “divide-by-zero” floating-point exception is raised.

Likewise, a range error occurs if the mathematical result of the function cannot be represented in an object of the specified type, due to extreme magnitude.

A floating result overflows if the magnitude of the mathematical result is finite but so large that the mathematical result cannot be represented without extraordinary rounding error in an object of the specified type. If a floating result overflows and default rounding is in effect, the function returns the value of macro HUGE_VAL, HUGE_VALF, or HUGE_ALL to the return type, with the same sign as the correct value of the function; if the integer expression math_errhandling & MATH_ERRNO is nonzero, the integer expression errno acquires the value ERANGE; if the integer expression math_errhandling & MATH_ERREXCEPT is nonzero, the “overflow” floating-point exception is raised.

The underflows if the magnitude of the mathematical result is so small that the mathematical result cannot be represented, without an extraordinary roundoff error, in an object of the specified type.³232) If the underflows, the function returns an implementation-defined value whose magnitude is no greater than the smallest normalized positive number in the specified type; if the integer expression math_errhandling & MATH_ERRNO is nonzero, or errno acquires the value ERANGE is implementation-defined; if the integer expression math_errhandling & MATH_ERREXCEPT is nonzero, the “underflow” floating-point exception is raised implementation-defined.

If a domain, pole, or range error occurs and the integer expression math_errhandling & MATH_ERRNO is zero.³233) then errno shall either be set to the value corresponding to the error or left unmodified. If no error occurs, errno shall be left unmodified regardless of the setting of math_errhandling.

232) The underflow here is intended to encompass both “gradual underflow” as in IEC 60559 and also “flush-to-zero” underflow.

233) Math errors are being indicated by the floating-point exception rather than by errno.