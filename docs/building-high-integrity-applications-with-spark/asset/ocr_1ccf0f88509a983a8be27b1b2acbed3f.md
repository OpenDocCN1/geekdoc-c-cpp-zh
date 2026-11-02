+   7.8 Write a full Ada version of the C helper function presented on page 267. An outline of how to proceed can be found at the end of Section 7.2. You may find it useful or appropriate to complete package Messages_Wrapper started on page 265. (Hint: The imported declaration of the underlying C function can be made local to the helper procedure. Thus, only the helper procedure needs to have SPARK_Mode set to Off.)

+   7.9 Pick a small C library that you have already written. Write a SPARK specification for your library and a demonstration program, in SPARK, that uses your library.

+   7.10 Repeat Exercise 7.6 for the case in which the package body is really a C library.

+   7.11 Define the phrases *effective read* and *effective write*. Why is it necessary to sometimes specify that reads and writes of external variables are always effective?

+   7.12 Write a package DIP that wraps a memory mapped register holding the state of eight DIP switches the user can adjust to provide input to your program. Your package should provide a subprogram for reading the switches and an appropriately declared external state abstraction.

+   7.13 The implementation of Get_Line in package Terminal suffers from two problems. First, a buffer of size zero will always cause the Insufficient_Space error to be returned. However, it should be possible to pass a zero-sized buffer successfully provided the user enters a blank line in response. Second, if the buffer is returned completely filled with characters, there is no way to distinguish between the case when the line is exactly the length of the buffer and when the user is trying to enter too much data. Fix these problems while maintaining SPARK’s proof of freedom from runtime error.