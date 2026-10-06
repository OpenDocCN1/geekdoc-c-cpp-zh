# CHAPTER 11 Exception Handling

```
using System;
using static System.Console;
class ReThrowDemo{
    static void Main()
    {
        try {
            WriteLine("Trying in Main() method");
            MethodA();
        } catch (Exception ae)
        {
            WriteLine("Caught in Main() method --\n {0}",
                ae.Message);
        }
        WriteLine("Main() is done");
    }
    private static void MethodA()
    {
        try {
            WriteLine("Trying in method A");
            MethodB();
        } catch (Exception)
        {
            WriteLine("Caught in method A");
            throw();
        }
    }
    private static void MethodB()
    {
        try {
            WriteLine("Trying in method B");
            MethodC();
        } catch (Exception)
        {
            WriteLine("Caught in method B");
            throw();
        }
    }
    private static void MethodC()
    {
        WriteLine("In method C");
        throw(new Exception("This came from method C"));
    }
}
```

**Figure 11-37** The ReThrowDemo program

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 02-200-202

524