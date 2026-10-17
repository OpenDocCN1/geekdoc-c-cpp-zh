# RUNTIME DEBUGGING

FIGURE 9.5 TestApp paused in the debugger

![](bbox=[0.28, 0.15, 0.86, 0.37])

For runtime debugging, Xcode integrates with GDB and the new LLDB debugger. Xcode provides a UI for managing breakpoints, controlling program execution, exploring the threads and stacks of the running application, accessing the debugger console, and more.

By default, all newly created Xcode projects are run in the debugger. The application will pause at the point of failure if it crashes or at any breakpoints you set if they’re encountered. The Debug area (Figure 9.5) appears when running an application with a debugger attached. The current instruction is highlighted with a green arrow in the Source Editor gutter.

![](bbox=[0.0, 0.56, 0.26, 0.68])

NOTE: Whether or not a debugger is attached to the running application is controlled by the active scheme. Schemes are covered in Chapter 14.