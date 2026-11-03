
Code three consecutive `getchar()` functions to read the characters. Format the result like this:

The three characters are 'a', 'b', and 'c'

where these characters — a, b, and c — would be replaced by the program’s input.

![](img/dcc0cd79d4a45cfce24fa49d85442884_101_0.png)

The program you create in Exercise 7-4 waits for three characters. The Enter key is a character, so if you type A, Enter, B, Enter, the three characters are A, the Enter key character, and then B. This input is valid, but what you probably want to type is something like ABC or PIE or LOL and then press the Enter key.

![](img/dcc0cd79d4a45cfce24fa49d85442884_101_1.png)

Standard input is stream-oriented. As I mention earlier in this chapter, don't expect your C programs to be interactive. Exercise 7-4 is an example of how stream input works; the Enter key doesn’t end stream input; it merely rides along in the stream, like any other character.

## Using the putchar() function

The output counterpart to `getchar()` is the `putchar()` function. It’s also prototyped in the `stdio.h` header file. The function serves the purpose of sending a single character to standard output. Here’s the format:

```c
int putchar(int c);
```

The function’s single argument is an integer value, in the preceding line of code. The argument can be a variable or a literal character, as in

```c
putchar('v');
```

The function returns the integer value of the character output, though this value need not be checked for simple character output, as shown in Listing 7-2.

### Putting putchar() to Work

```c
#include <stdio.h>

int main()
{
    int ch;
    putchar('A');
    putchar('B');
    putchar('C');
    putchar('\n');
    return 0;
}
```

```c
printf("Press Enter: ");
getchar();
ch = 'H';
putchar(ch);
ch = 'i';
putchar(ch);
putchar('!');
return(0);
}
```

This chunk of code uses the `getchar()` function to pause the program at Line 8. The input that's received isn't stored; it doesn't need to be. The compiler doesn't complain when you don't keep the value returned from the `getchar()` function (or from any function).

In Lines 9 through 12, single-character values are assigned to the `ch` variable, which works even though `ch` is an integer variable. The `putchar()` function then displays the changing value of variable `ch`.

In Line 13, `putchar()` displays a character literal, the exclamation point character. Again, the character must be enclosed in single quotes.

- **Exercise 7-5:** Create a new source file using the code shown in Listing 7-2. Build and run the program.

One weird thing about the output is that the final character isn't followed by a newline. That output can look awkward on a text display, so:

- **Exercise 7-6:** Modify the source code from Exercise 7-5 so that the newline character is output after the ! character.

## Working with character variables

*The `getchar()` and `putchar()` functions work with integers, but that doesn't mean you must shun character variables. When you work with characters in your code, use the `char` data type to store them, as shown in Listing 7-3.*

**LISTING 7-3: Character Variable Madness**

```c
#include <stdio.h>

int main()
{
    char a,b,c,d;

    a = 'W';
    b = a + 24;
    c = b + 8;
    d = '\n';
    printf("%c%c%c%c",a,b,c,d);
    return(0);
}
```

- **Exercise 7-7:** Create a new source code file using the code in Listing 7-3. Build and run the program.

The code declares four *char* variables at Line 5. These variables are assigned values in Lines 7 through 10. Line 7 is pretty straightforward. Line 8 uses math to set the value of variable *b* to a specific character, as does Line 9 for variable *c*. (Use Appendix A to look up a character’s ASCII code value.) Line 10 uses an escape sequence to set a character’s value, something you can’t type at the keyboard.

All those `%c` placeholders are stuffed into the *printf()* statement, but the output is, well, surprising.

- **Exercise 7-8:** Modify the code for Listing 7-3 so that variables *b* and *c* are assigned their character values directly using character literals held in single quotes.
- **Exercise 7-9:** Modify the source code again so that *putchar()*, not *printf()*, is used to generate output.

## Text I/O, but Mostly I

When character I/O is taken up a notch, it becomes text I/O. The primary text output functions are *puts()* and *printf()*. On the I side of I/O are text input functions, primarily *scanf()* and *fgets()*.

### Storing strings

When a program needs text input, it's necessary to create a place to store that text. Right away, you'll probably say, “Golly! That would be a string variable.” If you answered that way, I admire your thinking. You're relying upon your knowledge that text in C programming is referred to as a string.

Alas, you're wrong.

C lacks a string variable type. It does, however, have character variables. Queue up enough of them and you have a string. Or, to put it in programming lingo, you have an array of character variables.

Arrays are a big topic, covered in Chapter 12. For now, be open-minded about arrays and strings and soak in the goodness of Listing 7-4.

**LISTING 7-4: Stuffing a String into a char Array**

```c
#include <stdio.h>

int main()
{
    char prompt[] = "Press Enter to explode:";
    printf("%s",prompt);
    getchar();
    return(0);
}
```

Line 5 creates an array of char variables. An array is a gizmo that stores a bunch of the same data types all in a row. The char array is named prompt, which is immediately followed by empty square brackets. This is the Big Clue that the construction is an Array. The array is initialized, via the equal sign, to the text enclosed in double quotes.

The `printf()` statement in Line 7 displays the string stored in the prompt array. The `%s` conversion character represents a string.

In Line 8, `getchar()` pauses the program, anticipating the Enter key press. The program doesn't follow through by exploding anything, a task I leave up to you to code at a future date.

- **Exercise 7-10:** Create a new program using the source code from Listing 7-4. Build and run.
- **Exercise 7-11:** Modify the source code from Listing 7-4 so that a single string variable holds two lines of text; for example:

  ```
  Program to Destroy the World
  Press Enter to explode:
  ```

  Hint: Refer to Table 4-1, in Chapter 4.

- A string "variable" in C is really a character array.
- You can initialize a string to a char array when it's created, similarly to the way you initialize any variable when it's created. The format looks like this:

  ```c
  char string[] = "text";
  ```

  In the preceding line, string is the name of the char array, and text is the string assigned to that array.
- You cannot reassign or change a character array's contents by using a direct statement later in the code, such as

  ```c
  prompt = "This is just wrong.";
  ```

  Changing a string is possible in C, but you need to know more about arrays, string functions, and especially pointers before you make the attempt. Later chapters in this book cover these topics.
- See Chapter 6 for an introduction to the basic C language data types. The full list of C language data types is found in Appendix D.

### Introducing the scanf() function

For the input of specific data types, the `scanf()` function comes in handy. It's not a general-purpose input function, and it has some limitations, but it's great for testing code or grabbing values.

In a way, you could argue that `scanf()` is the input version of the `printf()` function. For example, it uses the same conversion characters (the `%` placeholder-things). Because of that, `scanf()` is quite particular about how text is input.

The `scanf()` function is prototyped in the `stdio.h` header file. Here's the format:

```c
int scanf(const char *restrict format, ...);
```

Scary, huh? Just ignore it for now. Here's my less frightening version of the format:

```c
scanf("placeholder", variable);
```

In this version, placeholder is a conversion character, and variable is a variable that matches the conversion character's data type. Unless variable is a string (char array), it's prefixed by the `&` operator.

Here are some `scanf()` examples:

```c
scanf("%d", &highscore);
```

The preceding statement reads an integer value from standard input into the variable highscore, an `int` variable.

```c
scanf("%f", &temperature);
```

The preceding `scanf()` statement waits for a floating-point value to be input, which is stored in the temperature variable.

```c
scanf("%c", &key);
```

In the preceding statement, `scanf()` accepts the first character read from standard input and stores it in the key variable.

```c
scanf("%s", firstname);
```

![](img/dcc0cd79d4a45cfce24fa49d85442884_106_0.png)

The `%s` placeholder is used to read in text, but only until the first whitespace character is encountered. So a space, a tab, or the Enter key terminates the string. Also, firstname is a char array, so it need not be prefixed by the `&` operator.

### Reading a string with scanf()

It's rare to use the `scanf()` function to read a string, because input is terminated at the first whitespace character. Still, it's worth a try.

To use the `scanf()` function to read in a chunk of text, the `%s` conversion character is used — just like in `printf()` but with input instead of output, as shown in Listing 7-5.
