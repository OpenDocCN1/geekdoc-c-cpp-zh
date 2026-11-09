# # 18 Debugging, Optimizing, and Managing Code

Xcode includes a powerful suite of tools for profiling, testing, and debugging code. You can test your application in three ways:

+   - Logging messages to the console.
+   - Setting breakpoints, single-stepping through code and checking property values in a debugging window.
+   - Using *instruments* — a collection of test tools that can report on memory use, thread states, application performance, object allocations, and memory leaks.

By default, Xcode supports two different build configuration options for both OS X and iPhone OS projects: Release and Debug. You can select these using the build drop-down menu at the top left of the Xcode window, as shown in Figure 18.1.

The Debug option creates a supporting symbol table. The Release build doesn't create this table, producing a much smaller binary.

On OS X, you can use the Release build as a final distribution version. On the iPhone, the default Release settings don't create a build for the App Store; they simply remove the symbol table. For information about creating a valid App Store release build, see Chapter 19.

# ### 18 In This Chapter

+   - Using the console and `NSLog`
+   - Debugging with breakpoints and the Debugger window
+   - Using *instruments*
+   - Managing code with Snapshots and Source Control