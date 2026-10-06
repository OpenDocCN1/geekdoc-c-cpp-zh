# Passing Parameters by Reference

method, TryParse() accepts an out parameter. The TryParse() method converts a string to the correct data type and stores the result in a variable if possible. If conversion is not possible, the method assigns 0 to the variable.

Figure 8-9 contains a program that uses the int.TryParse() method to convert entryString to an integer that is assigned to score. The differences from Figure 8-7 are the shaded change to the class name and the shaded call to the int.TryParse() method. The TryParse() method accepts two parameters: the string to be converted and the variable where the result is stored. The keyword out is required with the second parameter because the method receives its address and changes the value. Figure 8-10 shows two executions of the ConversionWithTryParse program. When the user's input cannot be converted correctly, the out parameter is assigned 0. Whether or not the user's input is in the correct format, the program continues and displays output of error messages.

```
using System.Console;
class ConversionWithTryParse{
    static void Main()
    {
        string entryString;
        int score;
        Write("Enter your test score >> ");
        entryString = ReadLine();
        int.TryParse(entryString, out score);
        WriteLine("You entered {0}", score);
    }
}
```

**Figure 8-9** The ConversionWithTryParse program

![](bbox=[0.104, 0.636, 0.473, 0.691])

![](bbox=[0.486, 0.636, 0.853, 0.691])

**Figure 8-10** Two typical executions of the ConversionWithTryParse program

The TryParse() method requires the receiving variable to be an out parameter for two reasons:

+   * The argument does not have an assigned value in the calling method.
* The method returns a Boolean value that indicates whether the conversion was successful and, so, it can return the score value.

Suppose you do not want a score to be assigned 0 if the conversion fails, because 0 is a legitimate score. Instead, you want to assign a -1 if the conversion fails. In that case you can use a statement similar to the following:

```
if(!int.TryParse(entryString, out score))
    score = -1;
```

opyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN-022-200-222