
Every CTYPE function returns an int value. The functions in Table 13-1 return logical TRUE or FALSE values; FALSE is 0, and TRUE is a non-zero value.

![](img/dcc0cd79d4a45cfce24fa49d85442884_210_0.png)

CTYPE functions are not real functions. No, they're macros defined in the ctype.h header file. Regardless, they look like functions and are used that way. (I write this note to prevent college sophomores from emailing me such corrections.)

## Testing characters

The CTYPE functions come in most handy when testing input, determining that the proper information was typed, or pulling required information out of junk. The code in Listing 13-1 illustrates how a program can scan text, pluck out certain attributes, and then output a summary of that information.

### LISTING 13-1: Text Statistics

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
    char phrase[] = "When in the Course of human events, it becomes necessary for one people to dissolve the political bands which have connected them with another, and to assume among the powers of the earth, the separate and equal station to which the Laws of Nature and of Nature's God entitle them, a decent respect to the opinions of mankind requires that they should declare the causes which impel them to the separation.";

    int index,alpha,space,punct;

    alpha = space = punct = 0;

        /* gather data */
    index = 0;
    while(phrase[index])
    {
        if(isalpha(phrase[index]))
            alpha++;
        if(isspace(phrase[index]))
            space++;
```

### LISTING 13-1: (continued)

```c
if(ispunct(phrase[index]))
    punct++;
    index++;
}

    /* print results */
    printf("\"%s\"\n",phrase);
    puts("Statistics:");
    printf("%d alphabetic characters\n",alpha);
    printf("%d spaces\n",space);
    printf("%d punctuation symbols\n",punct);

    return(0);
}
```

Listing 13-1 may seem long, but it's not; the phrase[] string declared at Line 6 can be anything you like — any text, a poem, or a filthy limerick. It should be long enough to have a smattering of interesting characters. Note that though the text wraps and indents in this text, you should just type one long line of text in your code.

This code also does something not yet presented in this book. I call it a gang initialization:

```
alpha = space = punct = 0;
```

Because each of these variables must be set to 0, you use multiple assignment operators on the same line and accomplish the task in one fell swoop.

The meat of the program's operation takes place starting after the gather data comment. A while loop steps through each character in the string. The condition for the while loop is phrase[index]. This evaluation is TRUE for each character in the array except for the last one, the null character, which evaluates to FALSE and stops the loop.

CTYPE functions are used in if statements as each character is evaluated at Lines 16, 18, and 20. I don't use if-else tests because every character must be checked. When a positive or TRUE match is found, a counter variable is incremented.

Exercise 13-1: Type the source code from Listing 13-1 into your editor. Build and run.

Exercise 13-2: Modify the source code from Listing 13-1 so that tests are also made for counting upper- and lowercase letters. Display those results as well.

Exercise 13-3: Add code to your solution to Exercise 13-2 so that a final tally of all characters in the text (the text's length) is displayed as the final statistic.

Many compilers add other is-CTYPE functions to their libraries. These functions are useful, such as isblank() to test for a space or tab, but they might not be available to every C compiler.

## Changing characters

The CTYPE functions begin with to are used to manipulate characters. The most common of these functions (the only two in the standard C library) are toupper() and tolower(), which come in handy when testing input. As an example, consider the typical yarn problem, illustrated in Listing 13-2.

### LISTING 13-2

### A yarn Problem

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
	char answer;

	printf("Would you like to blow up the moon? ");
	scanf("%c",&answer);
	answer = toupper(answer);
	if(answer=='Y')
		puts("BOOM!");
	else
		puts("The moon is safe");
	return(0);
}
```

Yarn is programmer-speak for a yes-or-no situation: The user is asked to type Y for Yes or N for No. Does the person have to type Y or y? Or can they type N or n, or would any non-Y key be considered No?

## TABLE 13-3 String Functions

| Function | What It Does |
|---|---|
| `strcat()` | Appends one string to another, creating a single string out of two. |
| `strncat()` | Appends a given number of characters from one string to the end of another. |
| `strchr()` | Searches for a character within a string. The function returns that character's position from the start of the string as a pointer. |
| `strcmp()` | Compares two strings in a case-sensitive way. If the strings match, the function returns 0. |
| `strncmp()` | Compares the first n characters of two strings, returning 0 if the given number of characters match. |
| `strcpy()` | Copies (duplicates) one string to another. |
| `strncpy()` | Copies a specific number of characters from one string to another. |
| `strlen()` | Returns the length of a string, not counting the \0 or NULL character at the end of the string. |
| `strrchr()` | Searches for a character within a string, but in reverse. The function returns the character's position from the end of the string as a pointer. |
| `strstr()` | Searches for one string inside another string. The function returns a pointer to the string's location if it's found. |

All the string functions in Table 13-3 require the `string.h` header file to be included with your source code:

```
#include <string.h>
```

![](img/dcc0cd79d4a45cfce24fa49d85442884_214_0.png)

On a Unix system, you can review all the string functions by typing the command `man string` in a terminal window.

![](img/dcc0cd79d4a45cfce24fa49d85442884_214_1.png)

Be aware of nonstandard string functions. For example, the `strcasecmp()` function compares strings regardless of text case, though this function isn't part of the standard C library. If you use such a function in your code, it may not compile on another computer system.

## Comparing text

Strings are compared by using the `strcmp()` function and its cousin `strncmp()`.

The string comparison functions return an `int` value based on the result of the comparison: 0 for when the strings are equal, or a higher or lower `int` value based on whether the first string's value is greater than (higher in the alphabet) or less than (lower in the alphabet) the second string. Most of the time, you just check for 0.

Listing 13-3 uses the strcmp() function in Line 13 to compare the initialized string password with whatever text is read at Line 11, which is stored in the input array. The result of this operation is stored in the match variable, which is used in an if-else decision tree at Line 14 to display the results.

### LISTING 13-3: Let Me In

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char password[]="taco";
    char input[15];
    int match;

    printf("Password: ");
    scanf("%s",input);

    match=strcmp(input,password);
    if(match==0)
        puts("Password accepted");
    else
        puts("Invalid password. Alert the authorities.");

    return(0);
}
```

**Exercise 13-7:** Type the source code from Listing 13-3 into your editor. Try out the program a few times to ensure that it accepts only taco as the proper password.

**Exercise 13-8:** Eliminate the match variable from your code in Exercise 13-7 and use the strcmp() function directly in the if comparison. This is the way most programmers do it.

## Building strings

The glue that sticks one string onto the end of another is the strcat() function. The term cat is short for concatenate, which means to link together. Here's how it works:

```c
strcat(first,second);
```
