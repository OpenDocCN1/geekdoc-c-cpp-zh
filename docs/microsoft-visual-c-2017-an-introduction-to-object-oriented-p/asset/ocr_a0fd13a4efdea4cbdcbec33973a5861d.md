# CHAPTER 11 Exception Handling

The TwoErrors class declares three integers and an integer array with three elements. In the Main() method, the try block executes, and at the first statement within the try block, an exception occurs because the denom in the division problem is zero. The try block is abandoned, and control transfers to the first catch block. Integer division by zero causes a DivideByZeroException, and because the first catch block receives that type of Exception, the message in first catch block appears along with the Message value of the Exception object. In this example, the second try statement is never attempted, and the second catch block is skipped. Figure 11-14 shows the output.

502

```
first catch block:
Attempted to divide by zero.
```

Figure 11-14 Output of the TwoErrors program

If you reverse the two statements within the try block in the TwoErrors program, the process changes. If you use the try block in Figure 11-15, division by zero does not take place because the invalid array access throws an exception first.

```
using System;
using static System.Console;
class TwoErrors2
{
    static void Main( )
    {
        int num = 13, denom = 0, result;
        int[] array = {22, 33, 44};
        try{
            result = array[num];
            result = num / denom;
        }catch(DivideByZeroException error)
{
            WriteLine("In first catch block: ");
            WriteLine(error.Message);
        }
        catch(IndexOutOfRangeException error)
{
            WriteLine("In second catch block: ");
            WriteLine(error.Message);
        }
    }
}
```

Figure 11-15 The TwoErrors2 program

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 02-200-202