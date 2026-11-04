```
```csharp
if (s.Length > 0)
{
    // Skip strings that aren't numbers.
    if (IsAllDigits(s))
    {
        // Convert the string into a 32-bit int.
        int num = 0;
        if (Int32.TryParse(s, out num))
        {
            Console.WriteLine("Next number = {0}", num);
            // Add this number into the sum.
            sum += num;
        }
        // If parse fails, move on to next number.
    }
}
}
// Output the sum.
Console.WriteLine("Sum = {0}", sum);
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
}
// IsAllDigits here.
}
```
```

The ParseSequenceWithSplit program begins by reading a string from the keyboard. The program passes the dividers array of char to the `Split()` method to indicate that the comma and the space are the characters used to separate individual numbers. Either character will cause a split there.

The program iterates through each of the smaller subarrays created by `Split()` using the foreach loop control. The program skips any zero-length subarrays. (This would result from two dividers in a row.) The program next uses the `IsAllDigits()` method to make sure that the string contains a number. (It won't, for instance, you type , .3 with an extra nondigit, nonseparator character.) Valid numbers are converted into integers and then added to an accumulator, sum. Invalid numbers are ignored. (I chose not to generate an error message to keep this short.)

Here’s the output of a typical run:

```
```text
Input a series of numbers separated by commas:
1,2, a, 3 4

Next number = 1
Next number = 2
Next number = 3
Next number = 4
Sum = 10
Press Enter to terminate...
```
```

The program splits the list, accepting commas, spaces, or both as separators. It successfully skips over the a to generate the result of 10. In a real-world program, however, you probably don’t want to skip over incorrect