# Section 13.2.3 Stream
Input/Output Classes and Objects

+   - The `basic_istream` **template (p. 580)** supports stream input operations.
+   - The `basic_ostream` **template (p. 580)** supports stream output operations.
+   - The `basic_iostream` template supports both stream input and stream output operations.
+   - The `istream` object `cin` is tied to the standard input device, normally the keyboard.
+   - The `ostream` object `cout` is tied to the standard output device, normally the screen.
+   - The `ostream` object `cerr` is tied to the standard error device, normally the screen. Outputs to `cerr` are **unbuffered (p. 581)**—each insertion to `cerr` appears immediately.
+   - The `ostream` object `clog` is tied to the standard error device, normally the screen. Outputs to `clog` are **buffered (p. 581)**.
+   - The C++ compiler determines data types automatically for input and output.