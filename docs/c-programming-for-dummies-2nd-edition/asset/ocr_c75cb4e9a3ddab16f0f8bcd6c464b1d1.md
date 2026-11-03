Don't let your eyeballs pop out of your head. Instead, consider my abbreviated format, which pretty much describes how printf() is used in this chapter:

```
printf("text");
```

In this definition, text is a string of text wedged between double quotes.

The printf() function requires the inclusion of the stdio.h header file.

The name printf() means print formatted, and the function really shows its horse-power in displaying formatted output. You can see this feature demonstrated in Chapter 13. The print part of the name hails back to the days when C programs sent their output primarily to printers, not to video displays.

![](bbox=[0.12, 0.39, 0.22, 0.43])

# Understanding the newline

Unlike the puts() function, the printf() function doesn't tack a newline character at the end of its output. A newline is the character that ends a line of text and directs the terminal to display any following text on the next line — the “new” line.

The following puts() function outputs the text Goodbye, cruel world on a line by itself:

```
puts("Goodbye, cruel world");
```

The following printf() function displays the text Goodbye, cruel world:

```
printf("Goodbye, cruel world");
```

After displaying the text, the cursor waits at the space after the d in world. Any additional text that's displayed appears on the same line, which is what you see for the output of Exercise 4-12:

```
Hickory, dickory, dock,The mouse ran up the clock.The clock struck one,The mouse ran down,Hickory, dickory, dock.
```

The code does exactly what you programmed it to do, albeit without fully knowing how printf() works. The results most likely aren't what you intended.

To make the printf() function display text on a line by itself, add the newline character to the end of the text string. Don't bother looking for the newline character on the keyboard; no, it's not the Enter key. You must use a C language escape sequence to type the newline character. Keep reading in the next section.