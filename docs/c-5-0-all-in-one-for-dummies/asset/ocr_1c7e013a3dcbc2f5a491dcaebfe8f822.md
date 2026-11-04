+   5. After announcing its intention with Now create nonstatic data member dynamically, **the `MyObject` constructor** creates an object of class `MyOtherObject` using the **`new` operator**, generating the second **`MyOtherObject` constructing message** as the **`MyOtherObject` constructor** is called.

+   6. Control returns to the `MyObject` constructor, which returns to `Main()`.

Job well done!

# Executing the constructor from the debugger

Executing the same program from the debugger is illuminating:

+   1. Rebuild the program: Choose the command `Build > Build DemonstrateCustomConstructor`.

You might also have to set the project as the startup project by right-clicking the `DemonstrateCustomConstructor` project and selecting **Set As Startup Project**.

![](bbox=[0.13, 0.45, 0.235, 0.55])

+   2. Before you start executing the program from the debugger, set a breakpoint at the `Console.WriteLine()` call in the **`MyOtherObject` constructor**.

To set a breakpoint, click in the gray trough on the left side of the editor window, next to the line at which you want to stop.

Figure 5-1 shows my display with the breakpoint set: The dark ball is in the trough.

+   3. Rather than choose `Debug > Start Debugging`, choose `Debug > Step Into` (or press F11).

Your menus, toolbars, and windows should change a bit, and then a bright yellow highlight appears on the opening curly brace in `Main()`.

+   4. Press F11 three more times and lightly rest the mouse pointer on the `localObject` variable (without clicking).

You're about to call the `MyObject` constructor. Your display should now look like the one shown in Figure 5-2. You can see that `localObject` is currently `null` under the cursor. The Locals window shows the same thing. (If Locals isn't visible, choose `Debug > Windows > Locals` to display it.)