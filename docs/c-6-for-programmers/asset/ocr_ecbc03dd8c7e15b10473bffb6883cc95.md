```
// calls Method2
static void Method1()
{
    Method2();
}

// calls Method3
static void Method2()
{
    Method3();
}

// throws an Exception containing an InnerException
static void Method3()
{
    // attempt to convert string to int
    try
    {
        int.Parse("Not an integer");
    }
    catch (FormatException formatExceptionParameter)
    {
        // wrap FormatException in new Exception
        throw new Exception("Exception occurred in Method3", formatExceptionParameter);
    }
}
```

exceptionParameter.ToString:
System.Exception: Exception occurred in Method3 ---> System.FormatException: Input string was not in a correct format.
at System.Number.StringToNumber(String str, NumberStyles options, NumberBuffer& number, NumberFormatInfo info, Boolean parseDecimal)
at System.Number.ParseInt32(String s, NumberStyles style, NumberFormatInfo info)
at System.Int32.Parse(String s)
at Properties.Method3() in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_05\Properties\Properties\Properties.cs:line 49
--- End of inner exception stack trace ---
at Properties.Method3() in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_05\Properties\Properties\Properties.cs:line 54
at Properties.Method2() in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_05\Properties\Properties\Properties.cs:line 40
at Properties.Method1() in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_05\Properties\Properties\Properties.cs:line 34
at Properties.Main() in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_05\Properties\Properties\Properties.cs:line 14

exceptionParameter.Message:
Exception occurred in Method3

Fig. 13.5 | Stack unwinding and Exception class properties. (Part 2 of 3.)