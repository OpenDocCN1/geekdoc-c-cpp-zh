WordStar is a word processor application that had a dominant market share during the early-to-mid 1980s. It used the high-order bit of an ASCII character for special formatting purposes.

WordStar would set the high order bit on the last character of a word to flag the location it can insert spaces to justify the right margin. It also set the high order bit on the spaces it inserts to know which spaces it can remove when it justifies the text. For example, it wouldn't want to remove the double space you put at the end of a sentence.

If you were to use a simple text editor to output the characters in a file created by WordStar, it might look something like this:

```
&Rt WritA · functio0 calleth find_strinA tô determinâ Iê onÂt characte0 c
strinÂt existØ insidâ anotheØ strinÂt THâ firsØ argumentØ tô thâ c
functio0 shoulâ bâ thâ characteØ strinâ thaô tô tô bâ searches anâ thâ c
secondâ argumentØ thâ strinâ wâ arâ interesteØ tô findingâ Iêt thâ c
functio0 findØ thâ specifick string' theô havâ 10 returñ thâ locatio0 c
10 thâ sourcâ strinâ wherâ thâ strinâ waØ foundâ Iê thâ Functio0 doeØ c
not find the string, then have it return -1. (25)
```

In fact, this is a question from an exam that I created with WordStar in 1986. I recently came across the file and wanted to view its contents. The reason for all of the gobbledeygook is due to the fact that WordStar has set the high order bit on many of the characters. Keep in mind that ASCII is actually a 7-bit code and never used the high-order bit to define a character. WordStar used this high order bit for it's own purposes!

So I created a program that reads the file one character at a time. The program creates a mask to turn off the high-order bit before outputting the character:

```
putchar(c & 0x7F);
```

This statement bit-ands the character with the mask 01111111, which effectively turns off the high-order bit.