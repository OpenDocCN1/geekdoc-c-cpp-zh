
## Programming Exercises

- 1. Find out what your system does with integer overflow, floating-point overflow, and floating-point underflow by using the experimental approach; that is, write programs having these problems. (You can check the discussion in Chapter 4 of limits.h and float.h to get guidance on the largest and smallest values.)
- 2. Write a program that asks you to enter an ASCII code value, such as 66, and then prints the character having that ASCII code.
- 3. Write a program that sounds an alert and then prints the following text:
```
Startled by the sudden sound, Sally shouted,
"By the Great Pumpkin, what was that!"
```
- 4. Write a program that reads in a floating-point number and prints it first in decimal-point notation, then in exponential notation, and then, if your system supports it, p notation. Have the output use the following format (the actual number of digits displayed for the exponent depends on the system):
```
Enter a floating-point value: 64.25
fixed-point notation: 64.250000
exponential notation: 6.425000e+01
p notation: 0x1.01p+6
```
- 5. There are approximately 3.156 × 10⁷ seconds in a year. Write a program that requests your age in years and then displays the equivalent number of seconds.
- 6. The mass of a single molecule of water is about 3.0×10⁻²³ grams. A quart of water is about 950 grams. Write a program that requests an amount of water, in quarts, and displays the number of water molecules in that amount.
- 7. There are 2.54 centimeters to the inch. Write a program that asks you to enter your height in inches and then displays your height in centimeters. Or, if you prefer, ask for the height in centimeters and convert that to inches.
- 8. In the U.S. system of volume measurements, a pint is 2 cups, a cup is 8 ounces, an ounce is 2 tablespoons, and a tablespoon is 3 teaspoons. Write a program that requests a volume in cups and that displays the equivalent volumes in pints, ounces, tablespoons, and teaspoons. Why does a floating-point type make more sense for this application than an integer type?

This page intentionally left blank

## Listing 4.1 The talkback.c Program

```
// talkback.c -- nosy, informative program
#include <stdio.h>
#include <string.h>      // for strlen() prototype
#define DENSITY 62.4     // human density in lbs per cu ft
int main()
{
    float weight, volume;
    int size, letters;
    char name[40];      // name is an array of 40 chars

    printf("Hi! What's your first name?\n");
    scanf("%s", name);
    printf("%s, what's your weight in pounds?\n", name);
    scanf("%f", &weight);
    size = sizeof name;
    letters = strlen(name);
    volume = weight / DENSITY;
    printf("Well, %s, your volume is %2.2f cubic feet.\n", name, volume);
    printf("Also, your first name has %d letters,\n", letters);
    printf("and we have %d bytes to store it.\n", size);

    return 0;
}
```

Running talkback.c produces results such as the following:

```
Hi! What's your first name?
Christine
Christine, what's your weight in pounds?
154
Well, Christine, your volume is 2.47 cubic feet.
Also, your first name has 9 letters,
and we have 40 bytes to store it.
```

Here are the main new features of this program:

- It uses an *array* to hold a *character string*. Here, someone's name is read into the array, which, in this case, is a series of 40 consecutive bytes in memory, each able to hold a single character value.
- It uses the `%s` *conversion specification* to handle the input and output of the string. Note that name, unlike weight, does not use the & prefix when used with `scanf()`. (As you'll see later, both `&weight` and name are addresses.)

The %s tells printf() to print a string. The %s appears twice because the program prints two strings: the one stored in the name array and the one represented by PRAISE. Running praise1.c should produce an output similar to this:

```
What's your name? Angela Plains
Hello, Angela. You are an extraordinary being.
```

You do not have to put the null character into the name array yourself. That task is done for you by scanf() when it reads the input. Nor do you include a null character in the character string constant PRAISE. We'll explain the #define statement soon; for now, simply note that the double quotation marks that enclose the text following PRAISE identify the text as a string. The compiler takes care of putting in the null character.

Note (and this is important) that scanf() just reads Angela Plains's first name. After scanf() starts to read input, it stops reading at the first whitespace (blank, tab, or newline) it encounters. Therefore, it stops scanning for name when it reaches the blank between Angela and Plains. In general, scanf() is used with %s to read only a single word, not a whole phrase, as a string. C has other input-reading functions, such as fgets(), for handling general strings. Later chapters will explore string functions more fully.

## Strings Versus Characters

The string constant "x" is not the same as the character constant 'x'. One difference is that 'x' is a basic type (char), but "x" is a derived type, an array of char. A second difference is that "x" really consists of two characters, 'x' and '\0', the null character (see Figure 4.3).

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_131_0.png)

Figure 4.3 The character 'x' and the string "x".

## The strlen() Function

The previous chapter unleashed the sizeof operator, which gives the size of things in bytes. The strlen() function gives the length of a string in characters. Because it takes one byte to hold one character, you might suppose that both would give the same result when applied to a string, but they don't. Add a few lines to the example, as shown in Listing 4.3, and see why.

```
Your name of 11 letters occupies 40 memory cells.
The phrase of praise has 31 letters and occupies 32 memory cells.
```

See what happens. The array name has 40 memory cells, and that is what the sizeof operator reports. Only the first 11 cells are needed to hold Serendipity, however, and that is what strlen() reports. The twelfth cell in the array name contains the null character, and its presence tells strlen() when to stop counting. Figure 4.4 illustrates this concept with a shorter string.

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_133_0.png)

Figure 4.4 The strlen() function knows when to stop.

When you get to PRAISE, you find that strlen() again gives you the exact number of characters (including spaces and punctuation) in the string. The sizeof operator gives you a number one larger because it also counts the invisible null character used to end the string. The program didn’t tell the computer how much memory to set aside to store the phrase. It had to count the number of characters between the double quotes itself.

As mentioned in Chapter 3, “Data and C,” the C99 and C11 standards use a %zd specifier for the type used by the sizeof operator. This also applies for type returned by strlen(). For earlier versions of C you need to know the actual type returned by sizeof and strlen(); typically that would be unsigned or unsigned long.

One other point: The preceding chapter used sizeof with parentheses, but this example doesn’t. Whether you use parentheses depends on whether you want the size of a type or the size of a particular quantity. Parentheses are required for types but are optional for particular quantities. That is, you would use sizeof(char) or sizeof(float) but can use sizeof name or sizeof 6.28. However, it is all right to use parentheses in these cases, too, as in sizeof (6.28).

The last example used strlen() and sizeof for the rather trivial purpose of satisfying a user’s potential curiosity. Actually, however, strlen() and sizeof are important programming tools. For example, strlen() is useful in all sorts of character-string programs, as you’ll see in Chapter 11.

Let’s move on to the #define statement.
