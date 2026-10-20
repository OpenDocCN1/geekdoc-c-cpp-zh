Obviously, you can make your stored procedure selection dialog as fancy as you would like. I opted for a simplistic design that permits typing the name of the file into an editable combo box. For ease of use, the combo box is prepopulated with any files in the current directory with a .psp extension.

# 8.1.2.2 Changes to the Command Dispatcher

Listing 8-1 is an abbreviated listing of CommandDispatcher's executeCommand() function including the logic necessary for parsing stored procedures. The omitted portions of the code appear in Section 4.5.2.

CommandDispatcher's executeCommand() Function Listing 8-1.

```
void
CommandDispatcher::CommandDispatcherInr
string& command)
{

// handle numbers, undo, redo, help in nested
```