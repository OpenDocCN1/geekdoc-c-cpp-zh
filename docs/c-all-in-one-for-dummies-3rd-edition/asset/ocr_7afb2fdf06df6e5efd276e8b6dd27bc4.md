+   - Next Instruction
+   - Step Out
+   - Step into Instruction
+   - Step Into
+   - Break Debugger
+   - Next Line
+   - Stop Debugger
+   - Run to Cursor
+   - Debugging Windows
+   - Debug/Continue
+   - Various Info

![](bbox=[0.253, 0.301, 0.874, 0.671])

**Figure 2-1:** The main Code::Blocks window shows your source code.

Figure 2-1 shows two special features you need to know in order to (successfully) debug applications. The first is the red octagon (like a stop sign), and the second is the yellow triangle. The red octagon is a breakpoint — a place where you want the debugger to stop. You add breakpoints to the Editing window by clicking the left side next to the instruction where you want to stop. When you click that spot again, the red octagon goes away, showing that you have cleared the breakpoint. You can place as many breakpoints as you want in the application, but you can place breakpoints only on instructions.

The yellow triangle is the instruction pointer, which shows the instruction that the debugger will execute next. As you tell the debugger to execute instructions, the yellow triangle moves. Whenever you start the application