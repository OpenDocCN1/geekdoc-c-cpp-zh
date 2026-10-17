# NAVIGATING THREADS AND STACKS

The Threads and Stacks navigator, which occupies the rest of the Debugger Bar, is used to switch between threads and navigate the call stack. It works in the same way as the Jump Bar. **Figure 9.7** shows the current call stack while TestApp is paused at a breakpoint in the `-applicationDidFinishLaunching:` method.

# WORKING IN THE CONSOLE

The console (**Figure 9.8**) displays the console output of your application and, while debugging, serves as a command-line interface to the debugger (whether you’re using GDB or LLDB).

The output can be filtered to show only debugger or target output using the pop-up menu in the upper-left corner of the console area. The debugger prompt is available only when the application is paused in debug mode. When the prompt is available, you can click to the right of the text prompt and input debugger commands, such as the GDB command `po` (print object).

The panel to the left of the console area, the Variables pane (**Figure 9.9**), shows the current variables and registers when debugger is paused. The pop-up button in the upper-left corner of the pane can be used to choose all variables, those that were recently accessed, or variables local to the current scope only.