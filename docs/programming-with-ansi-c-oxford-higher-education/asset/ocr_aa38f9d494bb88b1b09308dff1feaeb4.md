# Possible extensions

The program can be extended, with a little effort, to include the following features:

+   1. The format can become a little more portable. It is possible to provide a DLL, which reads from a file and sends the mark sheet out. There would be no input/output (IO) in the program, but only processing. In that case, the interface would be function-based. Functions could be called at runtime and mark sheets and marks of the students can be produced and updated as and when required. The calling program manages the IO.
+   
+   2. More generality can be provided for reading validated input by using wrapper classes.
+   
+   3. A student module such as subject can be provided to accept the roll numbers and names of the students so that we can print the names of students in place of roll numbers.
+   
+   4. The program can hold a mobile application programming interface, which will make it accessible as a mobile application.