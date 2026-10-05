# Key Commands in CUDA-GDB

Working within CUDA-GDB involves a repertoire of commands. Below is a rundown of essential commands that you will frequently use:

+   Sets a breakpoint at a specified location in your code. You can set a breakpoint at a specific line number or function. For CUDA kernels, you can also set a breakpoint for a specific thread by appending

+   Starts the execution of your CUDA application within CUDA-GDB.

+   Executes the next line of code in your application, stepping over any function calls.

+   Steps into a function call, allowing you to debug the function’s internal execution.

+   Continues running your application until it hits the next breakpoint.

+   Displays the value of a variable. For device variables, ensure that you’re inspecting them at a valid context during the device code execution.

+   Exits CUDA-GDB.

A typical debugging session would start with setting breakpoints, running the program, and then inspecting variable values or stepping through the code to understand the root cause of a bug.