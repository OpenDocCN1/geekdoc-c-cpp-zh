![](bbox=[0.05, 0.05, 0.95, 0.34])

# Figure B.4: The Watch view in Firebug

+   calls fibo() with an argument less than 5. Click over to the Breakpoints subtab, and uncheck your breakpoint to disable it.
+   
+   2. Then click the Step Out icon (the last one above the source pane) to let the code run away until it hits the previous stack trace level again. You should find yourself on the **return** line you had come from, with **base** being equal to 4 again.
+   
+   3. Repeating that operation will have you run back up the trace again and again (meaning the **base** watch is tracing back to values higher and higher), so that after a short while, you’ll notice the stack trace on the right is thinning up on the Stack subtab.
+   
+   4. When you’re tired of manually stepping and want to just resume normal execution, hit the Play button (the blue right arrow).

Note that all these stepping/running icons have shortcut keys, but these very widely based on the platform you’re running Firebug on. They’re usually mentioned in the icons’ tooltips, so just let your mouse hover on them to figure out these shortcuts.



Safari has been honoring its Web Inspector in recent years, and version 4.0 comes with a very decent feature set. (I hear current “nightlies” are making really good progress, too.) Although it is currently a bit subpar (with regard to Firebug) when it comes to DOM modification, its console and JavaScript debugger are certainly equivalent.

The Web Inspector’s Scripts section, with its console pane open, is shown in Figure B.5, on the following page (you can use one of the bottom-row icons to switch between the console and the Scripts view).