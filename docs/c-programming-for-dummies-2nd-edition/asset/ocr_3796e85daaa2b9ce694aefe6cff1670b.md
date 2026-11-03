Exercise 4-13: Re-edit the source code for your solution to Exercise 4-12, adding the newline character at the end of every printf() text string.

> printf("What!");

An escape sequence is required only when you need a character in a string and you cannot otherwise type it. For example, if you want to use the statement printf("What!"); you don't have to escape the exclamation point character because it doesn't otherwise mess up the text. You would, however, escape a newline, tab, or double-quote character.

Exercise 4-14: Create source code that uses the printf() function to display the following line of text:

> "Hey," said the snail, "I said no salt!";

Exercise 4-15: Modify the source code from Exercise 4-14 so that the puts() function is used instead of printf() to display the same text.

# Goofing up on purpose again

The section “Goofing up on purpose,” earlier in this chapter, introduces you to compiler errors. The compiler isn't the only part of the program creation process. The other major part is linking, and, yes, you'll find that the linker can detect errors as well, as shown in Listing 4-6.

# LISTING 4-6

# Another Horrible Mistake

```
#include <stdio.h>

int main()
{
    writeln("Another horrible mistake.");
    return(0);
}
```

Exercise 4-16: Type the source code from Listing 4-6 into the editor. Save. Build. And ...