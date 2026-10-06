# 2.2 Output, Input, and Variables

35

![Figure 2-6 IPO chart for the pay calculating program](2-6 IPO chart for the pay calculating program)

| IPO Chart for the Pay Calculating Program |
| Input | Processing | Output |
| Number of hours worked | Multiply the number of hours worked by the hourly pay rate. The result is the gross pay. | Gross pay |
| Hourly pay rate | | |

a to display screen output. In this book, we use the word Display to write pseudocode statements for displaying output on the screen. Here is an example:

Display "Hello world"

The purpose of this statement is to display the message Hello world on the screen. Notice that the word Display, we have written Hello world inside quotation marks. The quotation marks are not to be displayed. They simply mark the beginning and the end of the text that we wish to display.

Suppose your instructor tells you to write a pseudocode program that displays your name and address on the computer screen. The pseudocode shown in Program 2-1 is an example of such a program.

> Program 2-1
Display "Kate Austen"
Display "1234 Walmart Street"
Display "Asheville, NC 28899"

It is important for you to understand that the statements in this program execute in the order that they appear, from the top of the program to the bottom. This is shown in Program 2-7. If you translated this pseudocode into an actual program and ran it, the first statement would execute, followed by the second statement, and followed by the third statement. If you to visualize the way your program's output would appear on the screen, you should imagine something like that in Program 2-8. Each display statement produces a line of output.

> NOTE: Although this book uses the word Display for an instruction that displays screen output, some programmers use other words for this purpose. For example, some programmers use the word Print, and others use the word Write. Pseudocode has no rules that dictate the words that you may or may not use.