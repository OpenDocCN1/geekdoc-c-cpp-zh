

## LISTING 7-5: scanf() 吞掉一个字符串

```c
#include <stdio.h>

int main()
{
  char firstname[15];

  printf("Type your first name: ");
  scanf("%s", firstname);
  printf("Pleased to meet you, %s.\n", firstname);

  return(0);
}
```

### 练习 7-12

Type the source code from Listing 7-5 into your editor. Save, build, and run.

Line 5 declares a char array — a buffer to store a string — named firstname. The number in the brackets indicates the size of the array, or the total number of characters that can be stored there. The array isn’t assigned a value, so it’s created empty. Basically, the statement at Line 5 sets aside storage for up to 15 characters.

The scanf() function in Line 8 reads a string from standard input and stores it in the firstname array. The %s conversion character directs scanf() to look for a string as input, just as %s is a placeholder for strings in printf()’s output.

### 练习 7-13

Modify the source code from Listing 7-5 so that a second string is declared for the person’s last name. Prompt the user for their last name as well, and then display both names by using a single printf() function.

- The number in the brackets (refer to Line 5 in Listing 7-5) gives the size of the char array, or the length of the string, minus one. A 15-character array holds a string up to 14 characters long.
- The reason for a char array of size n holding n-1 characters is that all strings in C end with the null character, which is written as escape sequence \0. In C, as well as in other programming languages, the null character terminates a string. For strings obtained from standard input or those you create, you must remember to save one character of storage for the null character.
- The null character is not the same as the NULL pointer constant. Part 4 of this book covers pointers.

![](img/dcc0cd79d4a45cfce24fa49d85442884_107_0.png)

## 警告

The scanf() function as used in this chapter is considered insecure by modern coding standards. These exercises are good for learning C and practicing your coding. In the real world, however, programmers avoid using the scanf() function for input, because it can easily be exploited.

## 使用 scanf() 读取值

The scanf() function can do more than read strings. It can read in any value specified by a conversion character, as demonstrated in Listing 7-6.

## LISTING 7-6: scanf() 吃掉一个整数

```c
#include <stdio.h>

int main()
{
    int fav;

    printf("What is your favorite number: ");
    scanf("%d",&fav);
    printf("%d is my favorite number, too!\n",fav);
    return(0);
}
```

In Listing 7-6, the scanf() function reads an integer value from standard input. The %d conversion character is used, just like printf() — indeed, it's used again in Line 9. This character directs scanf() to look for an int value for variable fav.

### 练习 7-14

Write new source code using Listing 7-6. Build and run. Test the program by typing various integer values, positive and negative.

The ampersand (&) operator is used to prefix the second argument in the scanf() function. The & is the address-of operator. It's one of the advanced features in C, related to pointers. I avoid the topic of pointers until Chapter 18, but for now, know that an ampersand must prefix any variable specified in the scanf() function. The exception is an array, such as the firstname char array in Listing 7-5.

Try running the program again, but specify a decimal value, such as 41.9, or type text instead of a number.

The reason you see incorrect output is that scanf() is very specific. It fetches only the variable type specified by the conversion character. So if you want a floating-point value, you must specify a float variable and use the appropriate conversion character; %f, in this case.

### 练习 7-15

Modify the source code from Listing 7-6 so that a floating-point number is requested, input, and displayed.

![](img/dcc0cd79d4a45cfce24fa49d85442884_109_0.png)

- You don't need to prefix a char array variable with an ampersand in the scanf() function; when using scanf() to read in a string, just specify the string variable name.
- The scanf() function stops reading text input at the first whitespace character, space, tab, or Enter key.

## 使用 fgets() 进行文本输入

For a general-purpose text input function, one that reads beyond the first whitespace character, I recommend the fgets() function. Like most of the other text I/O functions, it's prototyped in the stdio.h header file. Here's the format:

```
char * fgets(char *restrict s, int n, FILE *restrict stream);
```

Frightening, no? The fgets() function is a file function, which reads text from a file, as in “file get string.” That’s how programmers talk after an all-nighter.

File functions are covered in Chapter 22, but because the operating system considers standard input like a file, you can use fgets() to read text from the keyboard.

Here's a simplified version of the fgets() function as it applies to reading text input:

```
fgets(string,size,stdin);
```

In this example, string is the name of a char array, a string variable; size is the number of characters to input plus one for the null character. Effectively, the size value is the same size as the char array. The final argument is the stdin constant, the name of the standard input device as defined in the stdio.h header file.

Listing 7-7 shows code that uses the fgets() function to read input.

## LISTING 7-7: fgets() 函数读取一个字符串

```c
#include <stdio.h>

int main()
{
    char name[10];

    printf("Who are you? ");
    fgets(name,10,stdin);
    printf("Glad to meet you, %s.\n",name);
    return(0);
}
```

### 练习 7-16

Type the source code from Listing 7-7 into your editor. Build and run.

The fgets() function in Line 8 reads text from standard input. The text is stored in the name array, which is set to a maximum of ten characters in Line 5. The value 10 is used as the second argument in the fgets() function to ensure that only nine characters are read, one less than the number specified. The final character in the name buffer is the null character, \0, which terminates the string.

The last argument in the fgets() function is stdin, the standard input device. This is the "file" from which input is read.

![](img/dcc0cd79d4a45cfce24fa49d85442884_110_0.png)

The char array must have one extra character reserved for the \0 at the end of a string. Its size must equal the size of input you need — plus one.

Here's how the program runs on my screen:

```
Who are you? Danny Gookin
Glad to meet you, Danny Goo.
```

Only the first nine characters of the text I typed in the first line are displayed. Why only nine? Because the tenth character must be the null character, \0, terminating the string. If the fgets() function were to read in ten characters instead of nine, the array would overflow and the program could malfunction.

If you type fewer than ten characters, you see that the Enter character is also stored in the string. This effect causes the period at the end of the printf() statement to appear alone on the following line:

```
Who are you? Danny
Glad to meet you, Danny
.
```

### 练习 7-17

Change the array size in the source code from Listing 7-7 to a constant value. Set the constant to allow only three characters input.

### 练习 7-18

Redo your solution for Exercise 7-13 so that fgets() rather than scanf() is used to read in the two strings.

You can read more about the reason fgets() is a preferred text input function in the nearby sidebar, “Avoid fgets()’s evil sibling gets().”

![](img/dcc0cd79d4a45cfce24fa49d85442884_111_0.png)

- The fgets() function as presented in this section reads text from the standard input device, not from the keyboard directly.
- The value returned by fgets() is the string that was input. In this book's sample code, this return value isn't used, although upon success, the string returned is identical to the information stored in the fgets() function's first argument, the char array variable.
- Chapter 13 offers more information about strings in C.

![](img/dcc0cd79d4a45cfce24fa49d85442884_111_1.png)

## 避免 fgets() 的邪恶兄弟 gets()

The original C language string-input function was gets(), for get-string. It took only a single argument, the character buffer or array into which text input was stored. The problem? No limit was set on this input, which means the buffer could easily overflow and wreak havoc in the computer. In fact, many early computer viruses were written specifically to exploit this weakness in the gets() function.

The gets() function is still available in the C library, though the compiler scolds you heavily for using it. Further, many compilers add warning text to any program created with the gets() function included in the code.

Bottom line: Don’t use gets() — use fgets() instead.

