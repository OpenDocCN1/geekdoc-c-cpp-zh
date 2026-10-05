![](bbox=[0.168, 0.078, 0.832, 0.355])

Apart from the timing, your result should be the same as that shown,
3.1414888, unless you've changed the NUMPOINTS, RADIUS, or SEED constants.

10. Close the console window and return to Visual Studio.

In the SerialPI method, the code in the for loop that generates the points and calculates their distance from the origin is an obvious area that can be parallelized. This is what you'll do in the next exercise.

To calculate pi by using parallel tasks

+   1. In Solution Explorer, double-click Program.cs to display the file in the Code and Text Editor if it is not already open.

+   2. Locate the ParallelPI method. It contains the same code as the initial version of the SerialPI method before you added the code to the try block to calculate pi.