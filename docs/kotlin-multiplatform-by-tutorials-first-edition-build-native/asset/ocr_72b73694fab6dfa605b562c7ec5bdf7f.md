from a third-party library. It navigates into that specific call if you have its source code or shows you the generated stubs if you don’t. Step into would probably skip it and halt only on your next instruction.

+   1. Step out from the current instruction. The rest of the code will execute, and the debugger will halt again when the method that was suspended executes.
+   2. Add a new watch. With this option, you can inspect any property or run any method that’s available on the current running scope.
+   3. The list of watchers. When the app halts, a list of variables that you can analyze is immediately shown. All the watchers that you add in the previous point will also be displayed here.

And that’s it! You can find the final project of the book in this appendix materials. Open it in Android Studio, add a breakpoint and run the app in debug mode. Try out the actions that you have available, follow a network request and inspect its response — and have fun. :]

# Debugging in Xcode

As you can see, debugging the shared module from Android Studio is simple. If you want to do the same thing in Xcode, it’s more...challenging. :]

If you want to debug the iOS UI, it uses the process you’re already familiar with. You just need to set a breakpoint, and the next time the app goes through that instruction it will halt.

But if you want to debug the shared module, it will take you a couple more steps. First, you’ll need to install the Kotlin Native Xcode Support plugin. You can find it on Touchlab GitHub repository or in the materials section of this appendix.

> **Note:** The last version of this plugin is from December 2020. Although Touchlab is currently providing support to the newest Xcode versions, there’s no guarantee, for now, that it will support future versions. Moreover, there are a couple of people reporting issues with Xcode 13.1 — although at the time of this writing, everything is working without any issue on that specific version.

# Installing the Kotlin Native Xcode Support plugin

To install the plugin, you need to first close Xcode. Then, open the command line and go to the repository root folder. There, enter:

```
```sh
./setup.sh
```
```