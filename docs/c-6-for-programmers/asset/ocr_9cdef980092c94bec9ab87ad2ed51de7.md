```
static void Main()
{
    var t1 = new Time2(); // 00:00:00
    var t2 = new Time2(); // 02:00:00
    var t3 = new Time2(21, 34); // 21:34:00
    var t4 = new Time2(12, 25, 42); // 12:25:42
    var t5 = new Time2(t4); // 12:25:42

    Console.WriteLine("Constructed with:\n");
    Console.WriteLine("t1: all arguments defaulted");
    Console.WriteLine("{0}", t1.ToUniversalString()); // 00:00:00
    Console.WriteLine("{0}", t1.ToString()); // 12:00:00 AM

    Console.WriteLine(
        "t2: hour specified; minute and second defaulted");
    Console.WriteLine("{0}", t2.ToUniversalString()); // 02:00:00
    Console.WriteLine("{0}", t2.ToString()); // 2:00:00 AM

    Console.WriteLine(
        "t3: hour and minute specified; second defaulted");
    Console.WriteLine("{0}", t3.ToUniversalString()); // 21:34:00
    Console.WriteLine("{0}", t3.ToString()); // 9:34:00 PM

    Console.WriteLine("t4: hour, minute and second specified");
    Console.WriteLine("{0}", t4.ToUniversalString()); // 12:25:42
    Console.WriteLine("{0}", t4.ToString()); // 12:25:42 PM

    Console.WriteLine("t5: Time2 object t4 specified");
    Console.WriteLine("{0}", t5.ToUniversalString()); // 12:25:42
    Console.WriteLine("{0}", t5.ToString()); // 12:25:42 PM

    // attempt to initialize t6 with invalid values
    try
    {
        var t6 = new Time2(27, 74, 99); // invalid values
    }
    catch (ArgumentOutOfRangeException ex)
    {
        Console.WriteLine("\nException while initializing t6:");
        Console.WriteLine(ex.Message);
    }
}
```

Constructed with:
t1: all arguments defaulted
00:00:00
12:00:00 AM

t2: hour specified; minute and second defaulted
02:00:00
2:00:00 AM