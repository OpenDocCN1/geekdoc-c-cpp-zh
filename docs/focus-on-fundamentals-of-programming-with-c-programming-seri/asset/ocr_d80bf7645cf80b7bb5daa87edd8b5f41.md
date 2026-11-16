# WordStar

WordStar was a word processor application that had a dominant market share during the early-to-mid 1980s. It used the high-order bit of an ASCII character for special formatting purposes.

WordStar would set the high order bit on the last character of a word to flag the location it can insert spaces to justify the right margin. It also set the high order bit on the spaces it inserts to know which spaces it can remove when it justifies the text. For example, it wouldn't want to remove the double space you put at the end of a sentence.

If you were to use a simple text editor to output the characters in a file created by WordStar, it might look something like this:

```
6$t WritA . functio$ calle$ find_$trinA tO determine$ iF on$t characteU$ c strinA$ exi$tUr in$ideA another$^ string$F TnA fir$ur^ argumen$t tOr^ thA$ c functio$ $hou$t bA thA characteU$ $trinA thaD tO tO bA $earches$ an$ thA$ c $econ$t argumeU$ thA$ $trinA wA ara interes$ed^ iOr finding$&r 1$t^ thA$ c functio$ findU thA $pecific $tring'+ 'theo havA 10 returU thA locatioU c 10 thA $ourcA $trinA wherA thA $trinA waU found$& 1F thA functio$ doeU c not find the $tring, then have it return -1. (25)
```

In fact, this is a question from an exam that I created with WordStar in 1986. I recently came across the file and wanted to view its contents. The reason for all of the gobbledeygook is due to the fact that WordStar has set the high order bit on many of the characters. Keep in mind that ASCII is actually a 7-bit code and never used the high-order bit to define a character. WordStar used this high order bit for its own purposes!

We can create a program that reads the file one character at a time. The program creates a mask to turn off the high-order bit before outputting the character:

```
putchar(c & 0x7f);
```

This statement bit-ands the character with the mask 01111111, which effectively turns off the high-order bit.