The %s tells printf() to print a string. The %s appears twice because the program prints two strings: the one stored in the name array and the one represented by PRAISE. Running praise1.c should produce an output similar to this:

```
What's your name? Angela Plains
Hello, Angela. You are an extraordinary being.
```

You do not have to put the null character into the name array yourself. That task is done for you by scanf() when it reads the input. Nor do you include a null character in the character string constant PRAISE. We'll explain the #define statement soon; for now, simply note that the double quotation marks that enclose the text following PRAISE identify the text as a string. The compiler takes care of putting in the null character.

Note (and this is important) that scanf() just reads Angela Plains's first name. After scanf() starts to read input, it stops reading at the first whitespace (blank, tab, or newline) it encounters. Therefore, it stops scanning for name when it reaches the blank between Angela and Plains. In general, scanf() is used with %s to read only a single word, not a whole phrase, as a string. C has other input-reading functions, such as fgets(), for handling general strings. Later chapters will explore string functions more fully.

# Strings Versus Characters

The string constant "x" is not the same as the character constant 'x'. One difference is that 'x' is a basic type (char), but "x" is a derived type, an array of char. A second difference is that "x" really consists of two characters, 'x' and '\0', the null character (see Figure 4.3).

![](bbox=[0.25, 0.68, 0.8, 0.75])

Figure 4.3 The character 'x' and the string "x".

# The strlen() Function

The previous chapter unleashed the sizeof operator, which gives the size of things in bytes. The strlen() function gives the length of a string in characters. Because it takes one byte to hold one character, you might suppose that both would give the same result when applied to a string, but they don't. Add a few lines to the example, as shown in Listing 4.3, and see why.