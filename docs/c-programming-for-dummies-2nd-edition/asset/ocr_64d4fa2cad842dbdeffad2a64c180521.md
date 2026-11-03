The code in Listing 17-6 outputs a value in binary, hexadecimal, and decimal and then shifts that value to the left, repeating the process. The print() statement at Line 13 uses the %X conversion character to output hexadecimal values.

Well, actually, the placeholder is %04X, which displays hex values using uppercase letters, four digits wide, and padded with zeros on the left as needed. The 0x text before the conversion character merely displays the output in standard C style.

# Exercise 17-13:

Type the code from Listing 17-6 into your editor. Save, build, and run.

# Exercise 17-14:

Change the value of variable b in Line 9 to read this way:

```
b = 0x11 ;
```

Save this change, build, and run.

![](bbox=[0.15, 0.57, 0.22, 0.68])

You can write hex values directly in your code. Prefix the values with 0x, followed by a valid hexadecimal number using either upper- or lowercase letters where required.

![](bbox=[0.15, 0.7, 0.2, 0.8])

# ONCE UPON A TIME, OCTAL WAS POPULAR

Another number format available in the C language is octal, or base 8. Octal was quite popular around the time Unix was developed, and many of the old, grizzled programmers league still enjoy tossing around octal values and doing octal-this or octal-that. C even sports an octal conversion character, %o, and an octal prefix, 0 (zero).

I've never used octal in any of my programs. Some older code may use it, and occasionally a function references octal values. So my advice is to be aware of octal, but don't bother to memorize anything.