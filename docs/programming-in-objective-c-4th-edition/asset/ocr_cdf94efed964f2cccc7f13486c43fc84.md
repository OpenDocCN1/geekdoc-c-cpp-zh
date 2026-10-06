```
All Output:
GNU gdb 6.3.30-2008 (Apple version gdb-1700.2) (Thu May 19 01:30:32 UTC 2011)
Copyright (C) 2008-2011 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are
welcome to change it in any way so long as you support the conditions.
Type "show copying" to see the conditions.
There is no warranty for GDB. Type "show warranty" for details.
GDB is configured for 'x86_64-apple-darwin' /dev/tty0
(Executing process /progi)
2011-07-07 22:41:56.717 progi[33404:903] Programming is fun
```

You're now done with the procedural part of compiling and running your first program with Xcode (whew!). The following summarizes the steps involved in creating a new program with Xcode:

+   1. Start the Xcode application.
2. If this is a new project, select File, New, New Project... or choose Create a New Xcode Project from the startup screen.
3. For the type of application, select Application, Command Line Tool, and click Next.
4. Select a name for your application and set its Type to Foundation. Make sure Use Automatic Reference Counting is checked. Click Next.
5. Select a name for your project folder, and a directory to store your project files in. Click Create.
6. In the left pane, you will see the file main.m (you might need to reveal it from inside the folder that has the product's name). Highlight that file. Type your program into the edit window that appears in the rightmost pane.
7. In the toolbar, select the middle icon under View. This will reveal the Debug area. That's where you'll see your output.
8. Build and run your application by clicking the Run button in the toolbar or selecting Run from the Product menu.

# Note