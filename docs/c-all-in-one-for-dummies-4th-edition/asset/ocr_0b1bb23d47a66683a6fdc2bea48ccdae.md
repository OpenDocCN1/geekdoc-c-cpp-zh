![](bbox=[0.26, 0.07, 0.87, 0.64])

**FIGURE 2-1:** The main Code::Blocks window shows your source code.

*Figure 2-1* shows two special features you need to successfully debug applications. The first is the red octagon, and the second is the yellow triangle. The red octagon is a *breakpoint* — a place where you want the debugger to stop. You add breakpoints to the Editing window by clicking the left side next to the instruction where you want to stop. When you click that spot again, the red octagon goes away, showing that you have cleared the breakpoint. You can place as many breakpoints as you want in the application, but you can place breakpoints only on instructions.

The yellow triangle is the instruction pointer, which shows the instruction that the debugger will execute next. As you tell the debugger to execute instructions, the yellow triangle moves. Whenever you start the application in debug mode, the yellow pointer automatically stops at each breakpoint. *Figure 2-1* shows how the debugger looks when the yellow triangle stops at a breakpoint.