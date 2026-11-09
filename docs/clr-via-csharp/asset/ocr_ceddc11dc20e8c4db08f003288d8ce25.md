believing that the `t` variable in `Main` must live until the end of the method. So, if a garbage collection were to occur, the garbage collector now thinks that `t` is still a root and that the `Timer` object that `t` refers to will continue to be reachable. The `Timer` object will survive the collection, and the `TimerCallback` method will get called repeatedly until `Console.ReadLine` returns and `Main` exits. This is easy to see. Just run the same executable file under a debugger, and you'll see that the `TimerCallback` method is called repeatedly!

Now, recompile the program from a command prompt, but this time, specify the C# compiler's `/debug+` compiler-line switch. When you run the resulting executable file, you'll now see that the `TimerCallback` method is called repeatedly—even if you don't run this program under a debugger! What is happening here?

Well, when the JIT compiler compiles a method, the JIT compiler looks to see if the assembly that defines the method contains the `System.Diagnostics.DebuggableAttribute` attribute with its `DebuggingModes` `DisableOptimizations` flag set. If the JIT compiler sees this flag set, it also compiles the method, artificially extending the lifetime of all variables until the end of the method. When you specify the `/debug+` compiler switch, the C# compiler emits this attribute and flag into the resulting assembly for you. Note, the C# compiler's `/optimize+` compiler switch can turn optimizations back on so this compiler switch should not be specified when performing this experiment.

The JIT compiler does this to help you with JIT debugging. You may now start your application normally (without a debugger), and if the method is called, the JIT compiler will artificially extend the lifetime of the variables to the end of the method. Later, if you decide to attach a debugger to the process, you can put a breakpoint in a previously compiled method and examine the variables.

So now you know how to build a program that works in a debug build but doesn't work correctly when you make a release build! Since no developer wants a program that works only when debugging it, there should be something we can do to the program so that it works all of the time regardless of the type of build.

You could try modifying the `Main` method to this:

```
```csharp
public static void Main() {
    // Create a Timer object that knows to call our TimerCallback
    // method once every 2000 milliseconds.
    Timer t = new Timer(TimerCallback, null, 0, 2000);

    // Wait for the user to hit <Enter>
    Console.ReadLine();

    // Refer to t after ReadLine (this gets optimized away)
    t = null;
}
```
```

However, if you compile this (without the `/debug+` switch) and run the resulting executable file (not under the debugger), you'll see that the `TimerCallback` method is still called just once. The problem here is that the JIT compiler is an optimizing compiler, and setting a local