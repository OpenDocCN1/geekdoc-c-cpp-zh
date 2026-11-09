
## Setting and using breakpoints

To set a breakpoint, select a line of code in Xcode's code editor and then choose Run ➤ Manage Breakpoints ➤ Add Breakpoint at Current Line. An arrow icon appears in the margin to the left of the line. Figure 18.7 shows the result of adding a breakpoint at the start of the `startCount:` and `stopCount:` methods.

**Figure 18.7**

Adding breakpoints: the code window displays a blue arrow icon in the margin next to each breakpoint. Here breakpoints have been added at two NSLog calls, but you can add a breakpoint on any line.

![](img/2b293e29fc15b0797f113b85dd429b6e_496_0.png)

Click Build and Debug, and the application builds and runs with added breakpoint information. When the code reaches a breakpoint, it pauses and the arrow icon displays a smaller extra brown arrow. The line with the breakpoint is highlighted, as shown in Figure 18.8.

You can do three things at a breakpoint:

- Review variables and properties
- Single-step through a method
- Continue execution

### Controlling breakpoint execution

The icons above the code editing window in Xcode control execution after a breakpoint and provide quick links to the Console and the Debugger window. The toolbar is shown in Figure 18.9. From left to right you can:

- Toggle breakpoints
- Continue execution to the next breakpoint, if there is one
- Step over a method or function
- Step into a method or function
- Step out of the current method or function
- Open the Debugger window
- Open the Console window

The step-over and step-into options single-step through code. Stepping out of a method or function “disappears” the execution marker when execution continues within OS X. (Unsurprisingly, you’re not allowed to view the OS X source code.) In your own code, execution may continue in another object.

**Figure 18.9**

The debugging toolbar.
The execution icons are only active while single-stepping after a breakpoint.

![](img/2b293e29fc15b0797f113b85dd429b6e_498_0.png)

### Setting conditional breakpoints

There are two sets of conditional breakpoints. The first is to define them in the Breakpoints window, shown in Figure 18.10. There is no menu option for this window in Xcode. It can only be opened by pressing ⌘+Alt+B on the keyboard.

If you’re familiar with gdb-compatible conditions, you can double-click under the Condition tab to enter them next to a selected breakpoint. In practice, this approach may be too clumsy to be useful. gdb’s conditional parser is limited, and conditional statements that test properties can become very complex. It’s often easier to use an alternative approach: add the conditional tests as temporary test code and bury a conventional static breakpoint inside them.

**Figure 18.10**

The Breakpoints window. You can selectively enable and disable breakpoints without removing them by clicking the check boxes in the second column.

![](img/2b293e29fc15b0797f113b85dd429b6e_499_0.png)

### Deleting breakpoints

To remove a single breakpoint, click on its line in Xcode and choose Run ▸ Manage Breakpoints ▸ Remove Breakpoint at Current Line. You can also press ⌘+\ as a keyboard shortcut.

Breakpoints tend to spread, so it can be useful to delete them all in a single operation. The simplest way to remove all breakpoints is to pause the application in the Console window and type delete breakpoints at the (gdb) prompt. Counterintuitively, this *does not delete* the breakpoints; it deactivates them. The effect is similar — they no longer do anything — but the breakpoints are still visible in the code.

To delete all breakpoints, open the Breakpoints window and press ⌘+A to select all of them. Press the Delete key to delete them. There is no menu option for this feature.

### Using the Debugger window

Often, you can debug directly in the code editor pane. The floating overlays and execution options give you enough information to find and fix simple problems. The Debugger window, shown again in Figure 18.11, is useful for more advanced problems, such as tracking crashes and monitoring object properties.

You can open the Debugger window three ways. The slow way is to choose Run > Debugger from the main Xcode menu. A faster way is to use the Shift+⌘+Y keyboard shortcut. The fastest and simplest way is to click the Debugger window icon in the Edit window toolbar, shown previously in Figure 18.9.

**Figure 18.11**

The Debugger window. The pane at the top left lists the execution stack. The pane at the top right lists every variable and data structure in the current object, and it can also list global values and the contents of the processor’s registers.

![](img/2b293e29fc15b0797f113b85dd429b6e_500_0.png)

### Using the stack trace

The execution stack appears in a pane at the top left. The stack lists the order in which methods and functions are called. After a crash, the item at the top of the stack caused the crash. This may be — and often is — an internal Cocoa object or function.

This pane doesn’t distinguish between Cocoa internals and your code. Typically most of the items in this list are internals. But you can look down the list to find the object, method, or function in your code that is likely to have caused a crash by feeding Cocoa invalid values.

## Using Instruments

Xcode includes a suite of performance tools that can report on almost every aspect of application performance. The tools are listed separately, but they run as a single tool with multiple snap-in options. To run a tool, choose Run > Performance Tool in Xcode. Xcode launches your application and launches the tool at the same time, linking the two so that the tool automatically starts collecting information. Figure 18.13 shows the instruments available in OS X. Figure 18.14 shows the smaller list available to iPhone developers.

> **TIP**
>
> You can combine options to create a customized tool that displays any combination of performance metrics. Choose Instrument > Build New Instrument. Each probe is a separate metric. Choose the metrics from the “of type” menu. Advanced developers can add customized scripting for each probe.

**Figure 18.13**

The instruments available to OS X developers. OS X developers can monitor threads, crashes, and multicore performance.

![](img/2b293e29fc15b0797f113b85dd429b6e_502_0.png)

**Figure 18.14**

The instruments available to iPhone OS developers. Both platforms support Leaks, Object Allocations, the CPU Sampler, and the Activity Monitor. Both also support Shark, which is an independent performance profiler.

![](img/2b293e29fc15b0797f113b85dd429b6e_503_0.png)

The generic Instruments tool runs as an event and value recorder. The top lane, or lanes, display a time trace of the metrics that are being monitored. Figure 18.15 shows a run of the Activity Monitor instrument, which tracks the performance and resource requirements of every process on a Mac.

All instruments use the same principle: the traces at the top of the window are graphed as the application runs. At the same time, the area under the trace lists numerical estimates of each feature.

You can save each run by choosing File > Save. You can't replay a timeline, but you can drag the cursor along it manually to review metric values at specific times. This is only occasionally useful. Typically, you look at metrics in real time and watch how they develop as you interact with the application.

**Figure 18.16**

Most instruments include filtering features. For the Time Profiler, the Call Tree options at the left can cut down a very long and cluttered list of OS X internals and force the instrument to show only the methods in your code.

![](img/2b293e29fc15b0797f113b85dd429b6e_505_0.png)

On the iPhone, memory management is one of the core problems, and the most useful instruments report object allocations and memory leaks. Object Allocations, shown in Figure 18.17, is perhaps the single most useful instrument for iPhone development. It displays a list of all allocated objects and the application’s total memory footprint.

To check for leaks, view the Live Bytes total for All Allocations. If it increases steadily as the application runs, or if it increases and doesn’t return to its original value after a user action, your application is leaking memory and will eventually crash. To find a leak, view the list of items under the # Living column. If this number is increasing, the object or function is leaking memory. Some leaks are built into iPhone OS and can’t be resolved. But this instrument can give you instant feedback about leaks in your code, saving you hours of development time.
