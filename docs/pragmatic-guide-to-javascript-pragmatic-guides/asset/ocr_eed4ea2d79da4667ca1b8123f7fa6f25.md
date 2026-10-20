![](bbox=[0.17, 0.062, 0.835, 0.376])

# Figure B.8: Debugging IE7 with breakpoints

+   6. Select the Empty Web Site option, and browse to whatever dummy directory you want to set it up in. Click OK.
+   7. Click the “Start debugging” menu option or icon (the green arrow).
+   8. This first time around, VWDE detects your project is not yet set up for debugging. It lacks a special Web.config file. A dialog box offers to create it for you or continue without debugging—obviously, leave the first option checked, and click OK.
+   9. You should see a development server on a dynamic port started in the taskbar, and your IE opens up on an empty directory listing named after your project’s directory (a warning bar may tell you the browser is working using the Intranet security zone, which is fine with us). You’re set to go!

Now that we’re all set up, just browse to our debugbench.html file any which way. Once opened, look into VWDE. On the right, in the Solution Explorer panel, you should see a Running documents branch with debugbench.html and debugbench.js listed. Double-click the latter.

You’re there! You can now set your breakpoint on line 2 the usual way (click in the gutter), switch back to your IE, and click the Fibo(20) button. You drop back to the debugger in stepping mode, as shown in Figure B.8. Voila!