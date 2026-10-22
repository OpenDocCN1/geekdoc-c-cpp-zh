
## Listing 11.5 The p_and_s.c Program

```
/* p_and_s.c -- pointers and strings */
#include <stdio.h>
int main(void)
{
    const char * mesg = "Don't be a fool!";
    const char * copy;

    copy = mesg;
    printf("%s\n", copy);
    printf("mesg = %s; &mesg = %p; value = %p\n", mesg, &mesg, mesg);
    printf("copy = %s; &copy = %p; value = %p\n", copy, &copy, copy);

    return 0;
}
```

## Note

Use %u or %lu instead of %p if your compiler doesn't support %p.

Looking at this program, you might think that it makes a copy of the string "Don't be a fool!", and your first glance at the output might seem to confirm this guess:

```
Don't be a fool!
mesg = Don't be a fool!; &mesg = 0x0012ff48; value = 0x0040a000
copy = Don't be a fool!; &copy = 0x0012ff44; value = 0x0040a000
```

But study the printf() output more carefully. First, mesg and copy are printed as strings (%s). No surprises here; all the strings are "Don't be a fool!".

The next item on each line is the address of the specified pointer. For this particular run, the two pointers mesg and copy are stored in locations 0x0012ff48 and 0x0012ff44, respectively.

Now notice the final item, the one we called value. It is the value of the specified pointer. The value of the pointer is the address it contains. You can see that mesg points to location 0x0040a000, and so does copy. Therefore, the string itself was never copied. All that copy = mesg; does is produce a second pointer pointing to the very same string.

Why all this pussyfooting around? Why not just copy the whole string? Well, ask yourself which is more efficient: copying one address or copying, say, 50 separate elements? Often, the address is all that is needed to get the job done. If you truly require a copy that is a duplicate, you can use the strcpy() or strncpy() function, discussed later in this chapter.

Now that we have discussed defining strings within a program, let's turn to strings provided by keyboard input.

If the input string is too long, you get buffer overflow, meaning the excess characters overflow the designated target. The extra characters might just go into unused memory and cause no immediate problems, or they may overwrite other data in your program, but those certainly aren’t the only possibilities. Here’s a sample run for which SLEN was reset to 5 to make it easier to overflow the buffer:

```
Enter a string, please.
warning: this program uses gets(), which is unsafe.
I think I’ll be just fine.
Your string twice:
I think I’ll be just fine.
I think I’ll be just fine.
Done.
Segmentation fault: 11
```

“Segmentation fault” doesn’t sound healthy, and it isn’t. On a Unix system, this message indicates the program attempted to access memory not allocated to it.

But C provides many paths for poor programming to lead to embarrassing and difficult to trace failures. Why, then, single out gets() for special mention? Probably because its unsafe behavior poses a security risk. In the past, people have taken advantage of system programming that uses gets() to insert and run code that compromised system security.

For a while, many in the C programming community have recommended banishing gets() from the programming vocabulary. The committee that created the C99 standard also published a rationale for the standard. This rationale acknowledged the problems with gets() and discouraged its use. However, it justified keeping gets() as part of the standard because it was a convenient function, in the right circumstances, and because it was part of much existing code.

The C11 committee, however, has taken a tougher view and has dropped gets() from the standard. However, a standard establishes what a compiler must support, not what it must not support. In practice, most compilers will continue to provide the function in the interests of backwards compatibility. But, as with the compiler we used, they don’t have to be happy about it.

## The Alternatives to gets()

The traditional alternative to gets() is fgets(), which has a slightly more complex interface and which handles input slightly differently. The C11 standard adds gets_s() to the mix. It’s a bit more like gets() and is more easily substituted into existing code as a replacement. However, it’s part of an optional extension to the stdio.h family of input/output functions, so C11 C compilers need not support it.

## The fgets() Function (and fputs())

The fgets() function meets the possible overflow problem by taking a second argument that limits the number of characters to be read. This function is designed for file input, which makes it a little more awkward to use. Here is how fgets() differs from gets():

- It takes a second argument indicating the maximum number of characters to read. If this argument has the value n, fgets() reads up to n-1 characters or through the newline character, whichever comes first.
- If fgets() reads the newline, it stores it in the string, unlike gets(), which discards it.
- It takes a third argument indicating which file to read. To read from the keyboard, use stdin (for standard input) as the argument; this identifier is defined in stdio.h.

Because the fgets() function includes the newline as part of the string (assuming the input line fits), it’s often paired with fputs(), which works like puts(), except that it doesn’t automatically append a newline. It takes a second argument to indicate which file to write to. For the computer monitor we can use stdout (for standard output) as an argument. Listing 11.7 illustrates how fgets() and fputs() behave.

## Listing 11.7 The fgets1.c Program

```
/* fgets1.c -- using fgets() and fputs() */
#include <stdio.h>
#define STLEN 14
int main(void)
{
    char words[STLEN];

    puts("Enter a string, please.");
    fgets(words, STLEN, stdin);
    printf("Your string twice (puts(), then fputs()):\n");
    puts(words);
    fputs(words, stdout);
    puts("Enter another string, please.");
    fgets(words, STLEN, stdin);
    printf("Your string twice (puts(), then fputs()):\n");
    puts(words);
    fputs(words, stdout);
    puts("Done.");

    return 0;
}
```

Here’s a sample run:

```
Enter a string, please.
apple pie
Your string twice (puts(), then fputs()):
apple pie

apple pie
Enter another string, please.
strawberry shortcake
Your string twice (puts(), then fputs()):
strawberry sh
strawberry shDone.
```

The first input, apple pie, is short enough that fgets() reads the whole input line and stores apple pie\n\0 in the array. So when puts() displays the string and adds its own newline to the output, it produces a blank output line after apple pie. Because fputs() doesn’t add a newline, it doesn’t produce a blank line.

The second input line, strawberry shortcake, exceeds the size limit, so fgets() reads the first 13 characters and stores strawberry sh\0 in the array. Again, puts() adds a newline to the output and fputs() doesn’t.

The fgets() function returns a pointer to char. If all goes well, it just returns the same address that was passed to it as the first argument. If the function encounters end-of-file, however, it returns a special pointer called the null pointer. This is a pointer guaranteed not to point to valid data so it can be used to indicate a special case. In code it can be represented by the digit 0 or, more commonly in C, by the macro NULL. (The function also returns NULL if there is some sort of read error.) Listing 11.8 shows a simple loop that reads and echoes text until fgets() encounters end-of-file or until it reads a blank line, indicated by the first character being a newline character.

## Listing 11.8 The fgets2.c Program

```
/* fgets2.c -- using fgets() and fputs() */
#include <stdio.h>
#define STLEN 10
int main(void)
{
    char words[STLEN];

    puts("Enter strings (empty line to quit):");
    while (fgets(words, STLEN, stdin) != NULL && words[0] != '\n')
        fputs(words, stdout);
    puts("Done.");

    return 0;
}
```
