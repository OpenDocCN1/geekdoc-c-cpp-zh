# 132 Chapter 3: More with Data Types

```
// Reverse the array
Array.Reverse(temp);

// Convert the array back to a string
// check if reverse string is the same
if (reverse == new string(temp))
{
    Console.WriteLine("{palindrome}" is a palindrome.");
}
else
{
    Console.WriteLine("{palindrome}" is NOT a palindrome.");
}
```

# OUTPUT 3.4

```
Enter a palindrome: NeverOddEven
"NeverOddEven" is a palindrome.
```

This example uses the new keyword; this time, it creates a new string from the reversed array of characters.

# Common Array Errors

This section introduced the three types of arrays: single-dimensional, multidimensional, and jagged. Several rules and idiosyncrasies govern array declaration and use. Table 3.3 points out some of the most common errors and helps solidify the rules. By reviewing the code in the Common Mistake column first (without looking at the Error Description and Corrected Code columns) as a way of verifying your understanding of arrays and their syntax.

# TABLE 3.3: Common Array Coding Errors

| Common Mistake | Error Description | Corrected Code |
| // 1. int numbers[]; | The square brackets for declaring an array appear after the data type, not after the variable identifier. | int[] numbers; |