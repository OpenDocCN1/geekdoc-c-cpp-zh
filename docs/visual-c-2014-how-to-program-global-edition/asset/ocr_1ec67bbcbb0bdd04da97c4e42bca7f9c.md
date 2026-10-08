# Exercises 229

```
b) if (m > 5)
if (n < 20)
{
  Console.WriteLine("RGB Mode");
}
else
{
  Console.WriteLine("CMYK Mode");
  Console.WriteLine("Greyscale");
}
```

5.29 (**Another Dangling-else Problem**) Based on the dangling-else discussion in Exercise 5.27 modify the code to produce the output shown in each part of the problem. Use proper indentation techniques. You might not make any additional changes other than inserting braces. We eliminated the indentation from the following code to make the problem more challenging. [Note: It's possible that no modification is necessary.]

```
if (y == 8)
if (x == 5)
Console.WriteLine("#####");
else
Console.WriteLine("$$$$$");
Console.WriteLine("&&&&&");")"
```

+   a) Assuming x = 5 and y = 8, the following output is produced:

00000
SSSSS
######

+   b) Assuming that x = 5 and y = 8, the following output is produced:

00000

+   c) Assuming that x = 5 and y = 8, the following output is produced:

00000
######

+   d) Assuming that x = 5 and y = 7, the following output is produced:

#####
SSSSS
######

5.30 (**Rectangle of Asterisks**) Write an app that prompts the user to enter the length and width of a rectangle, then displays a rectangle of that length and width made of asterisks. Your app should work for rectangles of all lengths between 1 and 15 and of all widths between 1 and 10. If the user enters a length less than 1 or greater than 15 and a width greater than 10, your app should display a rectangle with either length and width as 15 and 10, respectively.

5.31 (**Expanded form**) A number is in expanded form when it is expressed as the sum of the products of its digits and the place value of each digit. For example, 13023 can be expressed as (1 × 10000) + (3 × 1000) + (0 × 100) + (2 × 10) + (3 × 1). Write an app that reads a six-digit number and shows its expanded form. If the number is not six digits, display an error message, and ask the user to enter a new number. [Hint: Use the remainder and division operators to pick off the number’s digits one by one, from right to left]

5.32 (**Displaying the Decimal Equivalent of a Binary Number**) Write an app that inputs an integer containing only 0s and 1s (i.e., a binary integer) and displays its decimal equivalent. [Hint: Picking the digits of a binary number is similar to picking off a decimal number, which