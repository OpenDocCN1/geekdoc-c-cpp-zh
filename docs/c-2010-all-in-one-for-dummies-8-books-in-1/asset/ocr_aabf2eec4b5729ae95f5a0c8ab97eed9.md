# # Overloading an Inherited Method

As described in Chapter 3 of this minibook (look up overloading in the index), two or more methods can have the same name as long as the number or type of arguments differs (or as long as both differ).

> > ### **It's a simple case of method overloading**
> Giving two methods the same name is overloading, as in "Keeping them straight is overloading my brain."

The arguments of a method become a part of its extended name, as in this example demonstrates:

```
public class MyClass {
    public static void aMethod() {
        // Do something.
    }
    public static void aMethod(int) {
        // Do something else.
    }
    public static void aMethod(double d) {
        // Do something even different.
    }
    public static void Main(string[] args) {
        aMethod();
        aMethod(1);
        aMethod(2.0);
    }
```

C# can differentiate the methods by their arguments. Each of the calls in Main() accesses a different method.

The return type is not part of the extended name. You can't have two methods that differ only in their return types.

# ## Different class, different method

Not surprisingly, the class to which a method belongs is also part of its extended name. Consider this code segment:

```
public class MyClass {
    public static void aMethod1();
    public void aMethod2();
}
public class UrClass {
```