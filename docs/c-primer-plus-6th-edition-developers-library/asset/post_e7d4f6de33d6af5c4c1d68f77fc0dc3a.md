
## Listing 11.9 The fgets3.c Program

```c
/* fgets3.c -- using fgets() */
#include <stdio.h>
#define STLEN 10
int main(void)
{
    char words[STLEN];
    int i;

    puts("Enter strings (empty line to quit):");
    while (fgets(words, STLEN, stdin) != NULL
                && words[0] != '\n')
    {
        i = 0;
        while (words[i] != '\n' && words[i] != '\0')
            i++;
        if (words[i] == '\n')
            words[i] = '\0';
        else // must have words[i] == '\0'
            while (getchar() != '\n')
                continue;
        puts(words);
    }
    puts("done");
    return 0;
}
```

The loop

```c
while (words[i] != '\n' && words[i] != '\0')
    i++;
```

marches through the string until reaching a newline or null character, whichever comes first. If that character is a newline, the following if statement replaces it with a null character. Otherwise, the else part disposes of the rest of the input line. Here is sample run:

```
Enter strings (empty line to quit):
This
This
program seems
program s
unwilling to accept long lines.
unwilling
But it doesn't get stuck on long
But it do
```

What if the input line doesn’t fit? Then gets() isn’t safe; it can corrupt your data and compromise security. The gets_s() function is safe, but, if you don’t want the program to abort or otherwise exit, you’ll need to learn how to write and register special “handlers.” Also, if you manage to keep the program running, gets_s() disposes of the rest of the input line whether you want to or not. The fgets() function is the easiest to work with if the line doesn’t fit, and it leaves more choices up to you. If you want the program to process the rest of the input line, you can, as Listing 11.8 shows. If, instead, you want to dispose of the rest of the input line, you can do that, too, as Listing 11.9 shows.

So gets_s(), when input fails to meet expectations, is less convenient and flexible than fgets(). Perhaps that’s one reason that gets_s() is just an optional extension of the C library. And given that gets_s() is optional, using fgets() usually is the better choice.

## The s_gets() Function

Listing 11.9 presented one way to use fgets(): Read a whole line and replace the newline character with a null character, or read the part of a line that fits and discard the rest—sort of a gets_s() function without the extra baggage. No standard function meets that description, but we can create one. It’ll come in handy in later examples. Listing 11.10 shows one approach.

### Listing 11.10 The s_gets() Function

```c
char * s_gets(char * st, int n)
{
    char * ret_val;
    int i = 0;

    ret_val = fgets(st, n, stdin);
    if (ret_val)  // i.e., ret_val != NULL
    {
        while (st[i] != '\n' && st[i] != '\0')
            i++;
        if (st[i] == '\n')
            st[i] = '\0';
        else // must have words[i] == '\0'
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```

If fgets() returns NULL, indicating end-of-file or a read error, s_gets() skips the rest of the processing. Otherwise, it imitates Listing 11.9, replacing the newline character with a null character if the former is present in the string, and discarding the rest of the line otherwise. It then returns the same value fgets() returned. We’ll use this function in later examples.

Perhaps you are wondering what’s the rationale for discarding the rest of a too-long line. The problem is that if the remainder of the line is left in place, it becomes the input for the next read statement. This can, for example, cause the program to crash if the next read statement is looking for a type double value. Discarding the rest of the line keeps the read statements synchronized with the keyboard input.

Our s_gets() function isn’t perfect. Its most serious flaw is that it is silent about encountering input that doesn’t fit. It discards the extra input with neither the program nor the user being informed, thus closing off other options, such as having the user try again or finding more storage space. Another flaw is that it doesn’t cope with misuse such as being passed a size of 1 or less. But it’s good enough to serve as a gets() substitute for our examples.

## The scanf() Function

Let’s visit scanf() again. We’ve used scanf() with the %s format before to read a string. The chief difference between scanf() and gets() or fgets() lies in how they decide when they have reached the end of the string: scanf() is more of a “get word” than a “get string” function. The gets() function, as you’ve seen, takes in all the characters up to the first newline, as does fgets(), if the string is short enough. The scanf() function has two choices for terminating input. For either choice, the string starts at the first non-whitespace character encountered. If you use the %s format, the string runs up to (but not including) the next whitespace character (blank, tab, or newline). If you specify a field width, as in %10s, the scanf() collects up to 10 characters or up to the first whitespace character, whichever comes first (see Figure 11.3).

| Input Statement | Original Input Queue* | Name Contents | Remaining Queue |
| --- | --- | --- | --- |
| scanf("%s", name); | Fleebert□Hup | Fleebert | □Hup |
| scanf("%5s", name); | Fleebert□Hup | Fleeb | ert□Hup |
| scanf("%5s", name); | Ann□Ular | Ann | □Ular |

The □ represents the space character.

Figure 11.3 Field widths and scanf().

Recall that the scanf() function returns an integer value that equals the number of items successfully read or returns EOF if it encounters the end of file.

Listing 11.11 illustrates how scanf() works when you specify a field width.

### Listing 11.11 The scan_str.c Program

```c
/* scan_str.c -- using scanf() */
#include <stdio.h>
```

## String Output

Now let’s move from string input to string output. Again, we will use library functions. C has three standard library functions for printing strings: `puts()`, `fputs()`, and `printf()`.

### The `puts()` Function

The `puts()` function is very easy to use. Just give it the address of a string for an argument. Listing 11.12 illustrates some of the many ways to do this.

### Listing 11.12 The `put_out.c` Program

```c
/* put_out.c -- using puts() */
#include <stdio.h>
#define DEF "I am a #defined string."
int main(void)
{
    char str1[80] = "An array was initialized to me.";
    const char * str2 = "A pointer was initialized to me.";

    puts("I'm an argument to puts().");
    puts(DEF);
    puts(str1);
    puts(str2);
    puts(&str1[5]);
    puts(str2+4);

    return 0;
}
```

The output is this:

```
I'm an argument to puts().
I am a #defined string.
An array was initialized to me.
A pointer was initialized to me.
rary was initialized to me.
nter was initialized to me.
```

As with previous examples, each string appears on its own line because `puts()` automatically appends a newline when it displays a string.

This example reminds you that phrases in double quotation marks are string constants and are treated as addresses. Also, the names of character array strings are treated as addresses. The expression `&str1[5]` is the address of the sixth element of the array `str1`. That element contains the character `'r'`, and that is what `puts()` uses for its starting point. Similarly,

```c
char line[81];
while (gets(line))   // same as while (gets(line) != NULL)
    puts(line);
```

Recall that gets() returns the null pointer if it encounters end-of-file. The null pointer evaluates as zero, or false, so that terminates the loop. Or you can do this:

```c
char line[81];
while (fgets(line, 81, stdin))
    fputs(line, stdout);
```

With the first loop, the string in the line array is displayed on a line of its own because puts() adds a newline. With the second loop, the string in the line array is displayed on a line of its own because fgets() stores a newline. Note that if you mix fgets() input with puts() output, you’d get two newlines displayed for each string. The point is that puts() is designed to work with gets(), and fputs() is designed to work with fgets().

Of course we mention gets() only so that you’ll know how it works if you run across it in code and not to encourage you to use it.

### The `printf()` Function

We discussed printf() pretty thoroughly in Chapter 4, “Character Strings and Formatted Input/Output.” Like puts(), it takes a string address as an argument. The printf() function is less convenient to use than puts(), but it is more versatile because it formats various data types.

One difference is that printf() does not automatically print each string on a new line. Instead, you must indicate where you want new lines. Therefore,

```c
printf("%s\n", string);
```

has the same effect as

```c
puts(string);
```

As you can see, the first form takes more typing. It also takes longer for the computer to execute (not that you would notice). On the other hand, printf() makes it simple to combine strings for one line of printing. For example, the following statement combines Well, with the user’s name and a #defined character string, all on one line:

```c
printf("Well, %s, %s\n", name, MSG);
```

### The Do-It-Yourself Option

You aren’t limited to the standard C library options for input and output. If you don’t have these options or don’t like them, you can prepare your own versions, building on getchar().
