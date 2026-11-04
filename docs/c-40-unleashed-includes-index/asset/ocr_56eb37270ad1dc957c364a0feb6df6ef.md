Method group conversion refers to the capability of the compiler to figure out from context what method from the group is meant, based on the delegate type the method group gets assigned to. For more information, refer to the C# language specification, where all rules for method group conversion are outlined.

The two previous code fragments are completely identical from an intermediate language (IL) point of view, so it's time to take a look at how delegate instantiation works behind the scenes. Figure 17.7 illustrates this.

![](bbox=[0.15, 0.45, 0.65, 0.78])

FIGURE 17.7 Delegate instantiation from an IL perspective.

You've already seen the constructor function on the delegate type in the previous section, so no surprises there. It takes two arguments, one of which denotes the object instance on which to invoke the target method. Because we're using a static method in our example, there's no instance, and hence the ldnull instruction is emitted. The way to refer to a method is observed on the line following the ldnull instruction, using ldftn, which results in a native int. It's this native int value that points at the method and allows the CLR to call into the method when requested to do so by means of delegate invocation. Notice that I didn't lie about how the delegate is getting called. Line IL_0011 clearly shows a call to Invoke being emitted for the delegate invocation.

Based on the discussion here you will have guessed delegate instances can refer to instance methods as well:

```
static void Main() {
    var calc = new Calculator(); // with an Add instance method
    BinOp add = calc.Add;
    int three = add(1, 2); // calls the Add method on calc through the delegate
}
```