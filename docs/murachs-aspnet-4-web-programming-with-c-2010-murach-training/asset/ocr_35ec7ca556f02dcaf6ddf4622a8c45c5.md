# Commands in the Debug menu and toolbar

| Command | Toolbar | Keyboard | Function |
|---|---|---|---|
| Start/Continue |  | F5 | Start or continue execution of the application. |
| Break All |  | Ctrl+Alt+Break | Stop execution and enter break mode. |
| Stop Debugging |  | Shift+F5 | Stop debugging and end execution of the application. |
| Restart |  | Ctrl+Shift+F5 | Restart the entire application. |
| Show Next Statement |  |  | Display the next statement to be executed. |
| Step Into |  | F11 | Execute one statement at a time. |
| Step Over |  | F10 | Execute one statement at a time except for called methods. |
| Step Out |  | Shift+F11 | Execute the remaining lines in the current method. |

# Commands in the Code Editor window’s shortcut menu

| Command | Function |
|---|---|
| Run to Cursor | Execute the application until it reaches the statement that contains the insertion point. |
| Set Next Statement | Set the statement that contains the insertion point as the next statement to be executed. |
| Show Next Statement | Move the insertion point to the next statement that will be executed. |

# Description

+   - Once the application enters break mode, you can use the Step Into, Step Over, Step Out, and Run To Cursor commands to execute one or more statements and return to break mode.
+   - To alter the normal execution sequence of the application, you can use the Set Next Statement command. Just place the insertion point in the statement you want to execute next, issue this command, and click the Continue button to continue application execution.
+   - To stop an application that’s caught in a loop, switch to the Visual Studio window and use the Debug→Break All command.