+   4.1 Computation
4.2 Objectives and tools
4.3 Expressions
4.3.1 Constant expressions
4.3.2 Operators
4.3.3 Conversions
4.4 Statements
4.4.1 Selection
4.4.2 Iteration

+   4.5 Functions
4.5.1 Why bother with functions?
4.5.2 Function declarations
4.6 vector
4.6.1 Traversing a vector
4.6.2 Growing a vector
4.6.3 A numeric example
4.6.4 A text example
4.7 Language features

# 4.1 Computation

From one point of view, all that a program ever does is to compute; that is, it takes some inputs and produces some output. After all, we call the hardware on which we run the program a computer. This view is accurate and reasonable as long as we take a broad view of what constitutes input and output:

![](bbox=[0.17, 0.47, 0.72, 0.58])

The input can come from a keyboard, from a mouse, from a touch screen, from files, from other input devices, from other programs, from other parts of a program. “Other input devices” is a category that contains most really interesting input sources: music keyboards, video recorders, network connections, temperature sensors, digital camera image sensors, etc. The variety is essentially infinite.

To deal with input, a program usually contains some data, sometimes referred to as its data structures or its state. For example, a calendar program may contain lists of holidays in various countries and a list of your appointments. Some of that data is part of the program from the start; other data is built up as the program reads input and collects useful information from it. For example, the calendar program will probably build your list of appointments from the input you give it. For the calendar, the main inputs are the requests to see the months and days you ask for (probably using mouse clicks) and the appointments you give it to keep track of (probably by typing information on your keyboard). The output is the display