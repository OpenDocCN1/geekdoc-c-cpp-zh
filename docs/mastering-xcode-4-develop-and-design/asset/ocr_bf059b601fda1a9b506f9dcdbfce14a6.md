![](bbox=[0.13, 0.17, 0.61, 0.46])

FIGURE 15.5 A working WebView showing Google.com

That's it. Run the application. You might have to fish around for the second window (look behind the one you're familiar with), but it should be waiting there with Google loaded and ready for a search (Figure 15.5). Go ahead and try it out.

# NEGATIVE REINFORCEMENT

Now break it. To prove that the power to use a Web view comes from linking against WebKit.framework, unlink it. Navigate back to the TestApp target in the project, and then remove WebKit.framework from the Link build phase. Try running the app. I dare you. The app should terminate on launch on signal SIGABRT and spew a bunch of messages and a stack trace into the debugger console. The most interesting console message is the second one, that mentions "cannot decode object of class (WebView)," which is a good indicator you're referencing symbols from a library that hasn't been loaded (usually because you haven't linked against it). To fix it again, just add WebKit.framework back into your Link build phase.