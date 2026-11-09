# Figure 18.1

Selecting Debug and Release builds in Xcode. You can use the default Debug build settings for basic debugging. For more advanced techniques, you may need to modify the Debug configuration by hand.

![](bbox=[0.169, 0.205, 0.813, 0.597])

# Using the Console and NSLog

You’ll learn about debugging using the counter application from Chapter 8: it’s easy to modify but complex enough to introduce the theory and practice of profiling and debugging. Reload the application into Xcode, and click CounterAppDelegate.m. You’ll use this code as a testbed for the debugging and performance reporting tools built into Xcode.

# Getting started with NSLog

You’ve already worked with NSLog, but in this chapter you’ll use it in a structured way as a debugging aid. NSLog writes strings to the application’s console. The console is hidden in most Cocoa applications, but you can display it in Xcode while testing an application, and you can generate NSLog strings in the code to report variable values and application events.