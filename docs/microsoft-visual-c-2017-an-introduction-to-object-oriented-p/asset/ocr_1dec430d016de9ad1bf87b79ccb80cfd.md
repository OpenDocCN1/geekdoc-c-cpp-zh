# Avoiding Ambiguous Methods

When you overload a method, you run the risk of creating **ambiguous** methods—a situation in the compiler cannot determine which method to use. Every time you call a method, the compiler decides whether a suitable method exists; if so, the method executes, and if not, you receive an error message.

For example, suppose that you write two versions of a simple method, as in the program in Figure 8-23. The class contains two versions of a method named `SimpleMethod()`—one that takes a `double` and an `int`, and one that takes an `int` and a `double`.

```
using static System.Console;
class AmbiguousMethods {
    static void Main() {
        int iNum = 20;
        double dNum = 4.5;
        SimpleMethod(iNum, dNum); // calls first version
        SimpleMethod(dNum, iNum); // calls second version
        SimpleMethod(iNum, iNum); // error! Call is ambiguous.
    }
    private static void SimpleMethod(int i, double d) {
        WriteLine("Method receives int and double");
    }
    private static void SimpleMethod(double d, int i) {
        WriteLine("Method receives double and int");
    }
}
```

**Figure 8-23** Program containing an ambiguous method call

In the `Main()` of Figure 8-23, a call to `SimpleMethod()` with an integer argument first executes the first version of the method, and a call to `SimpleMethod()` with a `double` argument first and an integer argument executes the second version of the method. With each of these, the compiler can find an exact match for the method. However, if you call `SimpleMethod()` using two arguments, as in the shaded statement, an ambiguous situation arises because there is no exact match for the method call. Because the first integer could be promoted to a `double` (matching the second version of the overloaded method), or the second integer could be