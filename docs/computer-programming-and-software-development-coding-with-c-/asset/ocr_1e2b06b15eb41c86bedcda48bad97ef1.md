![](bbox=[0.12, 0.055, 0.59, 0.175])

You might wonder why Visual Studio created a namespace here that looks unnecessary, because if you think about it, this class exists just to contain the Main() method, and the Main() method is going to be called by the .NET platform, not by us. We're never going to write MyFirstProgram.Program.Main(), for example. So why bother with having a namespace here if we're not even using the name of this class? Isn't that overkill? Thing is, first, it's considered bad form to have a class without a namespace. Second, if you have a class without a namespace, C# still assigns the class to a default anonymous namespace. So in the end, you still have a namespace, so why not make it explicit at this point? By the way, while we're here, this class, let's rename it to something more appropriate, like CheckComfort.

![](bbox=[0.12, 0.61, 0.69, 0.73])

Now that we know about namespaces, let's fix this error.