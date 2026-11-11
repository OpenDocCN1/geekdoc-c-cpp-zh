There are a couple of other subtleties about autoboxing. First off, since wrapper class references can be null, it is possible for autounboxing to throw a `NullPointerException`:

```
Integer n = null;
System.out.println(2 * n); // throws NullPointerException
```

Also, if you mix Integer and Double types in a conditional expression, then the Integer value is unboxed, promoted to double, and boxed into a Double:

```
Integer n = 1;
Double x = 2.0;
System.out.println(true ? n : x); // prints 1.0
```

Finally, let us emphasize that boxing and unboxing is a courtesy of the *compiler*, not the virtual machine. The compiler inserts the necessary calls when it generates the bytecodes of a class. The virtual machine simply executes those bytecodes.

You will often see the number wrappers for another reason. The designers of Java found the wrappers a convenient place to put certain basic methods, such as those for converting strings of digits to numbers.

To convert a string to an integer, use the following statement:

```
int x = Integer.parseInt(s);
```

This has nothing to do with Integer objects—parseInt is a static method. But the Integer class was a good place to put it.

The API notes show some of the more important methods of the Integer class. The other number classes implement corresponding methods.

> > **CAUTION:** Some people think that the wrapper classes can be used to implement methods that can modify numeric parameters. However, that is not correct. Recall from Chapter 4 that it is impossible to write a Java method that increments an integer parameter because parameters to Java methods are always passed by value.

```
public static void triple(int x) // won't work
{
    x = 3 * x; // modifies local variable
}
```

Could we overcome this by using an Integer instead of an int?