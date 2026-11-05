```
static void Main()
{
    Timer objtimer = new Timer();

    /*A Timer class generates recurring events in an application.*/
    objtimer.Elapsed += new ElapsedEventHandler(
        delegate(object source, ElapsedEventArgs e)
        {
            Console.WriteLine("Event triggered at {0}", e.SignalTime);
        }
    );
    objtimer.Interval = 2000;// timer object is created every 2 seconds
    objtimer.Enabled = true;

    Console.ReadLine();
}
```

Input nil

# Output

Event triggered at (????? [Actual output would depend on system time.]

# 5.5 Method Overloading

This concept would be studied in Chapter - 8. Refer section 8.2.

# 5.6 Hiding Methods, Overriding Methods and Sealed Methods

These concepts would be studied in Chapter - 8 and Chapter - 9.

Refer section 8.1 for sealed method.

Refer section 9.3 for overriding.

Refer section 9.4 for method hiding.

AU : May-19

# 5.7 Unsafe Method or Unsafe Block

+   1. Unsafe code is code in which pointer manipulations have been done.
+   2. **Advantages of unsafe code in C#**
+      1. Performance and flexibility enhances because, by using pointer data can be accessed and manipulated in the most efficient way possible.
+      2. Compatibility is the major reason for using pointers as old windows APIs used the pointers extensively. Many third parties DLLs may supply their functionality