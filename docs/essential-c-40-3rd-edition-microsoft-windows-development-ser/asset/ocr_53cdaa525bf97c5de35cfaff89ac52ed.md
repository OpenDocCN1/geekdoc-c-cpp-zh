Because sentence structure varies among languages in different cultures, developers should be careful not to use the plus operator with strings that require localization. Composite formatting is preferred (refer to Chapter 1).

# Using Characters in Arithmetic Operations

When introducing the char type in the preceding chapter, I mentioned that even though it stores characters and not numbers, the char type is an integral type (“integral” means it is based on an integer). It can participate in arithmetic operations with other integer types. However, interpretation of the value of the char type is not based on the character stored within it, but rather on its underlying value. The digit 3, for example, contains a Unicode value of 0x33 (hexadecimal), which in base 10 is 51. The digit 4, on the other hand, contains a Unicode value of 0x34, or 52 in base 10. Adding 3 and 4 in Listing 3.5 results in a hexadecimal value of 0x167, or 103 in base 10, which is equivalent to the letter g.

# LISTING 3.5: Using the Plus Operator with the char Data Type

```
int n = '3' + '4';
char c = (char)n;
System.Console.WriteLine(c); // Writes out g.
```

Output 3.4 shows the results of Listing 3.5.

# Output 3.4:

9

You can use this trait of character types to determine how far two characters are from one another. For example, the letter f is three characters away from the letter c. You can determine this value by subtracting the letter c from the letter f, as Listing 3.6 demonstrates.

# LISTING 3.6: Determining the Character Difference between Two Characters

```
int distance = 'f' - 'c';
System.Console.WriteLine(distance);
```