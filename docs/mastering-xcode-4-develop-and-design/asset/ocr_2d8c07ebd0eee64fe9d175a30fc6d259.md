The most important reason for remembering this is that when you create your own queues with Grand Central Dispatch, you can give them a meaningful name so you can identify them clearly in the Debug navigator and (as you'll discover in Chapter 20) when using Instruments to profile your code.

# SUSPENDING THREADS

Grand Central Dispatch notwithstanding, threads are still threads, and the typical Cocoa application has several of them hanging around whether you created them or not. If you have created some threads of your own directly, chances are you did it wrong the first (several) times. You realize this because things are freezing, crashing, or just not acting right. It can be helpful in these cases to suspend a thread at runtime to keep it from interfering with other parts of your application or simply to examine it.

Why not just use breakpoints? Suspending a thread is different from using a breakpoint in two important ways. First, a breakpoint will pause execution regardless of the thread calling the instruction. That is, each time a breakpoint is encountered and execution is paused, the thread that hit the breakpoint could be any thread. Second, your goal may be to suspend only some background process your application is performing, not the entire application itself.

To suspend a thread is simple. Make sure you've paused the application in the debugger (either at a breakpoint or by using the Pause button in the Debugger Bar), then right-click (or Control-click) the thread in the Debug navigator and choose Suspend Thread from the menu. A red indicator will appear to the right of the suspended thread, showing that it is suspended. You could at this point resume the application (by hitting the Continue button in the Debugger bar) and the thread will remain paused—for good or ill—while your application goes about its business. To resume the thread, you'll need to be paused again, right-click (or Control-click) the paused thread, and choose Resume Thread from the menu.

> NOTE: Suspending a thread can cause unintended consequences that make your application act strangely at best or corrupt its data, freeze, or crash at worst. Pausing a thread that holds a lock, for example, could deadlock other threads. Use with caution.

![](bbox=[0.77, 0.795, 1.0, 0.935])