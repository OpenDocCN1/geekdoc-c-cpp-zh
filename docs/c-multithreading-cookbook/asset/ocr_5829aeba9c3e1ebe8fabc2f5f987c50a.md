As opposed to MS-DOS-based applications, Win32 applications are event-driven. They don't perform explicit function calls to obtain input. Instead, they wait for the system to pass input to them. The operating system passes all the messages designated for the application to the application window. The window has a function called a window procedure that the system calls whenever it has messages for the window. The window procedure processes the message and returns to the system.

Let's focus on WindowProc. We decided to process only two messages: WM_MOUSEMOVE, which is responsible for mouse move, and WM_COMMAND, which is responsible for button click. For mouse move, we use predefined macros, GET_X_LPARAM, to obtain the x-coordinate, and GET_Y_LPARAM, to obtain the y-coordinate. For button click, we use the lower 16 bits from the wParam to determine which child control raised the click. After we determine which control raised an event, we can perform any processing that we need for control. In our case, we use the Show msg button to display a message box and the Close me button to close the application.

# There's more...

Even though there are operating system specialized synchronization objects and routines, it is very handy and easy to use messages for synchronization whenever possible. If you run a separate thread asynchronously to do some task, you can use message passing to notify the main thread when the working thread finishes its task. In the examples to come, we will use message passing for communication between threads.

# Understanding a message queue

To understand message passing better, let's review the message queue. Every top-level window has its own message queue that is created by the operating system. In a multitasking environment, there are many applications executed at the same time with a lot of windows displayed on the user's screen. The operating system is processing a large number of messages while the user is pressing keyboard keys, clicking the mouse, or swiping the screen.

To demonstrate message passing along with the queue operations, let's review the following example. Let's assume that we need to perform complex drawings represented with a graphical plot with four axes. Every axis represents a certain mathematical calculation that needs graphical representation.

We will create an application where one thread is responsible for a drawing based on the calculation performed by another thread, while the other thread is responsible for the calculation. Let's assume that the thread calculation time is smaller than the drawing time that is needed for a portion of the plot that has to be drawn.