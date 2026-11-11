Note that the `TalkingClock` class no longer needs to store a beep instance field. It simply refers to the beep parameter variable of the `start` method.

Maybe this should not be so surprising. The line

```java
if (beep) . . .
```

is, after all, ultimately inside the `start` method, so why shouldn’t it have access to the value of the beep variable?

To see why there is a subtle issue here, let’s consider the flow of control more closely.

+   1. The `start` method is called.
+   2. The object variable `listener` is initialized by a call to the constructor of the inner class `TimePrinter`.
+   3. The listener reference is passed to the `Timer` constructor, the timer is started, and the `start` method exits. At this point, the beep parameter variable of the `start` method no longer exists.
+   4. A second later, the `actionPerformed` method executes if `(beep) . . .`

For the code in the `actionPerformed` method to work, the `TimePrinter` class must have copied the beep field as a local variable of the `start` method, before the beep parameter value went away. That is indeed exactly what happens. In our example, the compiler synthesizes the name `TalkingClock$1TimePrinter` for the local inner class. If you use the `ReflectionTest` program again to spy on the `TalkingClock$1TimePrinter` class, you will get the following output:

```
class TalkingClock$1TimePrinter
{
    TalkingClock$1TimePrinter(TalkingClock, boolean);

    public void actionPerformed(java.awt.event.ActionEvent);

    final boolean val$beep;
    final TalkingClock this$0;
}
```

Note the boolean parameter to the constructor and the `val$beep` instance variable. When an object is created, the beep value is passed into the constructor and stored in the `val$beep` field. The compiler detects access of local variables, makes matching instance fields for each one, and copies the local variables into the constructor so that the instance fields can be initialized.