So far, all of the examples have shown how to write a method that takes an arbitrary number of Int32 parameters. How would you write a method that takes an arbitrary number of parameters where the parameters could be any type? The answer is very simple: modify the method's prototype that it takes an Object[] instead of an Int32[]. Here's a method that displays the Type of every object passed to it.

```
public sealed class Program {
    public static void Main() {
        DisplayTypes(new Random(), "Jeff");
    }

    private static void DisplayTypes(Object[] objects) {
        if (objects != null) {
            foreach (Object o in objects) {
                Console.WriteLine(o.GetType());
            }
        }
    }

```

Running this code yields the following:
System.Object
System.Random
System.String
System.Int32

> Important Be aware that calling a method that takes a variable number of arguments incurs an additional performance hit unless you explicitly pass null. After all, an array object must be allocated on the heap, the array's elements must be initialized, and the memory must ultimately be garbage collected. To reduce the performance hit you might want to consider defining a few overloaded methods that do not use the params keyword. For some examples, look at the System. String class's Concat method, which has the following overloads:

```
public sealed class String : Object, {
    public static string Concat(Object arg0);
    public static string Concat(Object arg0, Object arg1);
    public static string Concat(Object arg0, Object arg1, Object arg2);
    public static string Concat(params[] args);

    public static string Concat(string str0, string str1);
    public static string Concat(string str0, string str1, string str2);
    public static string Concat(string str0, string str1, string str2, string str3);
    public static string Concat(params[] values);
}
```

As you can see, the Concat method defines several overloads that do not use the params keyword. These versions of the Concat method are the most frequently called overloads, and these overloads exist in order to improve performance for the most common scenarios. The overloads that use the params keyword are for the less common scenarios; these scenarios will suffer a performance hit, but fortunately, they are rare.