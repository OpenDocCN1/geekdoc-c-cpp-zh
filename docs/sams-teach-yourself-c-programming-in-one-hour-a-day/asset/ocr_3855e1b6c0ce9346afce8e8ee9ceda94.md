# LESSON 8 Using Numeric Arrays

```
Month 2 = $100.65
Month 3 = $3421.04
Month 4 = $34.67
Month 5 = $5.60
Month 6 = $1267.00
Month 7 = $200.00
Month 8 = $45.21
Month 9 = $23.12
Month 10 = $187.90
Month 11 = $12.54
Month 12 = $3.00
```

Yearly expenses ▼ $5346.40

# Analysis

When you run expenses.c, the program prompts you to enter expenses for months 1 through 12. The values you enter are stored in an array. You must enter a value for each month. After the 12th value is entered, the array contents display onscreen.

The flow of the program is similar to what you've seen before. Line 1 starts with a comment that describes what the program does. Notice that the name of the program, expenses.c, is included. When the name of the program is included in a comment, you know which program you're viewing. This is helpful when you're reviewing printouts of a listing.

Line 5 contains an additional comment explaining the variables declared. In line 7, an array of 13 elements is declared. In this program, only 12 elements are needed, for each month, but 13 have been declared. Line 9 declares a total variable that will be used after the array is filled. The for loop on lines 15 through 19 ignores element 0. This lets the program use elements i through i12, which relate directly to the 12 months. Going back to line 8, a variable, count, is declared and used throughout the program as a counter and an array index.

The program's main() function begins on line 11. As stated earlier, this program uses a for loop to print a message and accept a value for each of the 12 months. Notice that on line 18, the scanf function uses an array element. On line 7, the expenses array was declared as float, so %f is used. The address-of-operator (*) is also placed before the array element, just as if it were a regular float variable and not an array element.

Lines 23 through 27 contain a for loop that prints the values just entered. As discussed in the last lesson, adding .2 between the percent sign and the f (%.2f) prints a floating number with two digits to the decimal, a format that makes sense when printing financial totals. Additional formatting commands are covered in more detail in Lesson 14, "Working with the Screen, Printer, and Keyboard."