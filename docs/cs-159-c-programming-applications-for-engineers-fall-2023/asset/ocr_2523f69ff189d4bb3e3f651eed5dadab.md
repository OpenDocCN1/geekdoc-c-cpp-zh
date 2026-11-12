# Comparing Two Strings

+   Just as we cannot assign one string to another, neither can we successfully compare two strings for equality using the equality and relational operators.

# Example:

| Code | Explanation |
| :--- | :--- |
| `char str1[SIZE];`
`char str2[SIZE];`
`getString(str1);`
`strcpy(str2, str1);`
`if(str1 == str2)`
`{`
`printf("The strings are equal!\\n");`
`}` | One would assume if the equality operator compares contents of strings that ANY value entered would lead to the equal statement being printed every time the previous code segment is executed.

**What is output?** None.

**What does that tell us about what is being compared when using relational or equality operators with two strings?**

The comparison using the equality operator is testing memory addresses and not the string data. |

# Alternative - using the string.h function strcmp

This third function from the string.h library will accept two strings as parameters and will return an integer indicating how the two strings are different. Two strings storing the same data have no difference.

| Scenario | Explanation |
| :--- | :--- |
| Enter your string -> company
Enter your string -> corporate
Compare result: -5 | In the first example it is the third element where the first difference is found. This difference value is returned from the `strcmp` function. The element of the second parameter is subtracted from the element of the first parameter. |
| Enter your string -> company
Enter your string -> companion
Compare result: 16 | Enter your string -> ABC123
Enter your string -> ABC123
Compare result: 0 |
| Enter your string -> ABC123
Enter your string -> ABC123
Compare result: -18 | It is NOT the sum of the differences that is used when calculating the difference, it is the FIRST difference in order from lowest index to highest. |
| Enter your string -> ABC12
Enter your string -> ABC123
Compare result: -51 | What if the two strings do not have the same number of elements? |
| Enter your string -> ABC123
Enter your string -> AbC123
Compare result: -32 | Does character case have significance? |