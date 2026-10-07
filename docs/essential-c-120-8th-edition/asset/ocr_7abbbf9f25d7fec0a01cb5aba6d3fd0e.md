# 60 Chapter 2: Data Types

```
LISTING 2.5: Exponential Notation
Console.WriteLine(6.023E23F);
```

OUTPUT 2.4

```
6.023E+23
```

# BEGINNER TOPIC

# Hexadecimal Notation

Usually, you work with numbers that are represented with a base of 10, meaning there are 10 symbols (0–9) for each place value in the number. If a number is displayed with hexadecimal notation, it is displayed with a base of 16 numbers, meaning 16 symbols are used: 0–9, A–F (in lowercase). Therefore, 0x000A corresponds to the decimal value 10 and 0x002A corresponds to the decimal value 42, being 2 × 16 + 10. The actual number is the same. Switching from hexadecimal to decimal, or vice versa, does not change the number itself—just the representation of the number.

Each hex digit is four bits, so a byte can represent two digits.

In all discussions of literal numeric values so far, we have covered only base 10 type values. C# also supports the ability to specify hexadecimal values. To specify a hexadecimal value, prefix the value with 0x and then use any hexadecimal series of digits, as shown in Listing 2.6.

```
LISTING 2.6: Hexadecimal Literal Value
//Display the value 42 using a hexadecimal literal
Console.WriteLine(0x002A);
```

Output 2.5 shows the results of Listing 2.6. Note that this code still displays 42, 0x002A.

Starting with C# 7.0, you can also represent numbers as binary values (see Listing 2.7).