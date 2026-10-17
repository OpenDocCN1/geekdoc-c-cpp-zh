```
#Listing03_07.pl
#Multiple statements on one line
print "\nListing03_07.pl works.";                    #single statement
print "\nMultiple statements on one line";          #single statement
#Multiple statements on one line follow
;;;
print "\nReady to add more lines!"; print "\nAnd more lines...";"!";
```

Figure 3.6 illustrates the output. Notice that the interpreter reads the statements on the final line without problems. The output appears on separate lines because the \n forces the string following it onto a new line.

![](bbox=[0.149, 0.35, 0.625, 0.499])

**Figure 3.6**  
Successive statements on a single line cause no errors.

> Although composing code with several statements on one line creates no syntax errors, consider that many experienced programmers regard this as poor programming style. Experienced programmers often insist that you should place no more than one statement on each line of code.

# Escape Sequences

In most of the code samples shown so far, the quoted text used with the `print()` function begins with a slash character followed by an “n” character (`\n`). This combination of characters causes a line return to be inserted into the output of the `print()` function. The slash can be used with several other characters as well. The slash and the character that accompanies it are together called an *escape sequence*. An escape sequence escapes the normal execution of your program. It makes it so that the Perl interpreter interprets a character like any other text character rather than trying to process it as a language feature. To see how this works, consider the following code sample:

```
#Listing03_08.pl
#Different uses of the escape sequence
```