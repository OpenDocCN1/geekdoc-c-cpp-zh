Figure 6–2 shows the results of an execution of Example 6–2 when 14 and 33 are entered as the range of values.

![](bbox=[0.185, 0.16, 0.912, 0.374])

**FIGURE 6–2** Example of output from user-entered loop boundaries

With Example 6–2, what happens when the user enters a larger value for the `startValue` than the value entered for `endValue`? If you answered the loop body will not get executed, even one time, you are correct. Because the conditional expression evaluates to false, the body is skipped and the lines following the loop are executed.

When you are requesting input from the user, you always run the risk that invalid characters may be entered. You have seen a number of examples that test input using the `TryParse()` method. You saw statements such as

```
if (int.TryParse(inStringValue, out integerValue) == false)
    Console.WriteLine("Invalid input - 0 recorded for end value");
```

If a character such as “b” is entered by the user and stored in `inStringValue`, `TryParse()` returns false, indicating it was not able to do the conversion. When `TryParse()` returns false, the conditional expression evaluates to true. Then zero is stored in `integerValue` as a side effect of the `TryParse()` method not being able to properly do the conversion. There are instances when it is not acceptable to just print an error message. You may want to make sure valid characters are entered before proceeding with additional statements. Instead of just testing to see whether `TryParse()` is able to effectively do the conversion, you could use the `TryParse()` method as your conditional expression for a loop as illustrated in Example 6–3.