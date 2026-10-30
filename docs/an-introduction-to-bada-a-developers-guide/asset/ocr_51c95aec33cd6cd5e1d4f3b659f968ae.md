![](bbox=[0.35, 0.07, 0.65, 0.6])

Figure 2.6 BuddyFix showing in the main menu.

# 2.1.5 Standard Output

One useful view in the Eclipse IDE is the Output pane. When you launch an app in the Simulator, the system logs an ‘Application started’ message, and when you close the app, the system logs an ‘Application finished’ message:

```
0010.200, INFO, P26, T-01, A-01, OspMain (24) > Application started.
0014.030, INFO, P26, T-01, A93, OspMain (39) > Application finished.
```

Between these log points, you can output your own printf-like logging statements to trace your app’s behaviour at runtime, using bada’s logging macros, AppLog(), AppLogDebug(), and AppLogException(). For example, to output a simple log message, add the line:

```
AppLog("This message will display in the output view");
```

Log files can be exported to simple text files with a .log suffix. In the Output pane, once your application is running, select the second icon on the left (as indicated in Figure 2.7); a dialog is invoked that allows saving the output into a log file on your development machine.