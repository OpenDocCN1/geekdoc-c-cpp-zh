low-level, so it should just throw exceptions as needed — or just pass on any exceptions that occur in the methods it calls. We recommend looking up the call chain to see which method might be a good location for a handler.

![](bbox=[0.1, 0.24, 0.2, 0.36])

As you move up the call chain, ask yourself the questions in the earlier section “Some questions to guide your planning.” What would be the consequences if `FixNamespaceLine()` threw an exception? That depends on how its result is used higher up the chain. Also, how dire would the results need to be? If you can’t “fix” the namespace line for the current file, does the user lose anything major? Maybe you can get away with an occasional unfixed file, in which case you might choose to “swallow” the exception at some level in the call chain and just notify the user of the unprocessed file. Or maybe not. You get the idea. We discuss these and other exception-handling options in the article “Responding to an Exception” on http://csharp102.info.

The moral is that correctly setting up exception handlers requires some analysis and thought.

![](bbox=[0.1, 0.54, 0.2, 0.66])

However, keep in mind that any method call can throw exceptions — for example, the application could run out of memory, or the assembly it’s in might not be found and loaded. You can’t do much about that.

![](bbox=[0.1, 0.68, 0.2, 0.78])

# How to find out which methods throw which exceptions

To find out whether calling a particular method in the .NET class libraries, such as `String.IndexOf()` — or even one of your own methods — can throw an exception, consider these guidelines:

+   - **Visual Studio provides immediate help with tooltips.** When you hover the mouse pointer over a method name in the Visual Studio editor, a yellow tooltip window lists not only the method’s parameters and return type but also the exceptions it can throw.
+   - **If you have used XML comments to comment your own methods.** Visual Studio shows the information in those comments in its IntelliSense tool tips just as it does for .NET methods. If you documented the exceptions your method can throw (see the previous section), you see them in a tooltip. The article “Getting Help in Visual Studio” on http://csharp102.info shows how to use XML comments, and the FactorialException example you can download illustrates documenting `Factorial()` with XML comments. Plug in the `<exception>` line inside your `<summary>` comment to make it show in the tooltip.
+   - **The Help files provide even more.** When you look up a .NET method in Help, you find a list of exceptions that the method can throw, along with additional descriptions not provided via the yellow Visual Studio tooltip. To open the Help page for a given method, click the method name in

![](bbox=[0.1, 0.82, 0.2, 0.92])