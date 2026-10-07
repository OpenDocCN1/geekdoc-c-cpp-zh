# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# Annex K

# (normative)

# Bounds-checking interfaces

# K.1 Background

+   1 Traditionally, the C Library has contained many functions that trust the programmer to provide output arrays big enough to hold the result being produced. Not only do these functions check that the arrays are big enough, they frequently lack the information needed to perform such checks. While it is possible to write safe, robust, and error-free code using the existing library, the library tends to promote programming styles that lead to disastrous failures if a result is too big for the provided array.

+   2 A common programming style is to declare character arrays large enough to handle most practical cases. However, if these arrays are not large enough to handle the resulting strings, data can be written past the end of the array overwriting other data and program structures. The program never gets any indication that a problem exists, and so never has a chance to recover or fail gracefully.

+   3 Worse, this style of programming has compromised the security of computers and networks. Buffer overflows can be exploited to run arbitrary code with the permissions of the vulnerable (defective) program.

+   4 If the programmer writes runtime checks to verify lengths before calling library functions, then these runtime checks frequently duplicate work done inside the library functions, which duplicate strings as a side effect of doing their job.

+   5 This annex provides alternative library functions that promote safer, more secure programming. The alternative functions verify that output buffers are large enough for the intended result and return a failure indicator if they are not. Data is never written past the end of an array. All string results are null terminated.

+   6 This annex addresses problem that complicates writing robust code: functions that are not reentrant because they return pointers to static objects owned by the function. Such functions can be troublesome since a previously returned result can change if the function is called again, perhaps by another thread.