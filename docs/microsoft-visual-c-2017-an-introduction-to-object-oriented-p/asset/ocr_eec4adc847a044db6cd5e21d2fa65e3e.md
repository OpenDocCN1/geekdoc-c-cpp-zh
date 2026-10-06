# TWO TRUTHS & A LIE

# Overloading Methods

+   1. The following methods are overloaded:
   private static void MethodA(int a)
   private static void MethodA(double b)

+   2. The following methods are overloaded:
   private static void MethodC(int c)
   private static void MethodD(int c)

+   3. The following methods are overloaded:
   private static void MethodE(int e)
   private static void MethodE(int e, int f)

> different parameter lists.
The false answer is #2. Overloaded methods must not have the same name

# You Do It

Overloading Methods

In the next steps, you overload methods that correctly triple a parameter that might be an integer or a string.

+   1. Start a new program named OverloadedTriples, and create a method that triples and displays an integer parameter as follows:

```
private static void Triple(int num)
{
    const int MULT_FACTOR = 3;
    WriteLine("{0} times {1}={2}\n",
    num, MULT_FACTOR, num * MULT_FACTOR);
}
```

(continues)