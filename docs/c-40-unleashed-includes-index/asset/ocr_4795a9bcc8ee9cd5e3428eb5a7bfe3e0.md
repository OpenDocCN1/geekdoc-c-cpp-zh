```
static class StaticBoom {
    static int x = 0;
    static int y = 1 / x;

    public static int X { get { return x; } }
}
```

![](bbox=[0.05, 0.3, 0.75, 0.6])

FIGURE 23.15 A static constructor blowing up.

The InnerException of the TypeInitializationException contains the original exception object (in our case, a DivideByZeroException caused by the initialization of the static field y). To see the source of the exception with your own eyes, enable first-chance exceptions and observe the exception being thrown on the line that initializes y. The call stack at this point is most interesting, as shown in Figure 23.16.

![](bbox=[0.06, 0.87, 0.6, 0.97])

FIGURE 23.16 The place where the static constructor gets called.