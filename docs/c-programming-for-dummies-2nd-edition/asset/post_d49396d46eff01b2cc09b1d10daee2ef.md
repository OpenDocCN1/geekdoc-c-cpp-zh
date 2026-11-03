
## Initializing an array

As with any variable in C, you can initialize an array when it's declared. The initialization requires a special format, similar to this statement:

```
int highscore[] = { 750, 699, 675 };
```

The number in the square brackets isn't necessary when you initialize an array, as shown in the preceding example. The reason is that the compiler is smart enough to count the elements and allocate the array's storage automatically.

**Exercise 12-6:** Write a program that displays the stock market closing numbers for the past five days. Use an initialized array, marketclose[], to hold the values. The output should look something like this:

```
Stock Market Close
Day 1: 24164.95
Day 2: 24107.08
Day 3: 24643.63
Day 4: 24400.93
Day 5: 23728.53
```

**Exercise 12-7:** Write a program that uses two arrays. The first array is initialized to the values 10, 12, 14, 15, 16, 18, and 20. The second array is the same size but not initialized. In the code, fill the second array with the square root of each of the values from the first array. Output the results.

## Playing with character arrays (strings)

You can create an array using any of the C language's data types. A char array, however, is a little different when it's a string.

As with any array, you can declare a char array initialized or not. The format for an initialized char array can look like this:

```
char letters[] = { 'c', 'a', 't' };
```

This array declaration is for a 3-element character array, containing the letters c, a, and t. This example is a character array, not a string.

```
char pet[] = "cat";
```

The preceding array declaration creates a string. The initialization text is enclosed in double quotes. Further, because a string literal is used, the compiler automatically adds the terminating null character: '\0'. This addition is what makes the array a string and not a collection of characters — an important concept to understand.

Here is the same string declaration written as individual characters:

```
char cat[] = { 'c', 'a', 't', '\0' };
```

Each array element in the preceding line is defined as its own char value, including the '\0' character that terminates the string. (I believe that you'll find the double-quote method far more effective at declaring strings.)

The code in Listing 12-3 plods through the char array one character at a time. The index variable is used as, well, the index. The while loop spins until the '\0' character at the end of the string is encountered. A final putchar() function (in Line 14) kicks in a newline.

### LISTING 12-3: Displaying a char Array

```
#include <stdio.h>

int main()
{
    char sentence[] = "Random text";
    int index;

    index = 0;
    while(sentence[index] != '\0')
    {
        putchar(sentence[index]);
        index++;
    }
    putchar('\n');
    return(0);
}
```

Exercise 12-8: Type the source code from Listing 12-3 into your editor. Build and run the program.

The while loop in Listing 12-3 works like many string display routines found in the C library. These functions probably use pointers instead of arrays, which is a topic unleashed in Chapter 18. Beyond that bit o' trivia, you could replace Lines 8 through 14 in the code with the line

```
puts(sentence);
```

or even with this one:

```
printf("%s\n",sentence);
```

![](img/dcc0cd79d4a45cfce24fa49d85442884_194_0.png)

When the char array is used as a function's argument, as shown in the preceding line, the square brackets aren't necessary. If they're included, the compiler believes that you screwed up.

## Working with empty char arrays

Just as you can declare an empty, or uninitialized, float or int array, you can create an empty char array. You must be precise, however: The array's size must be one character greater than the maximum length of the string to account for the terminating null character. Also, you have to ensure that whatever input fills the array doesn't exceed the array's size.

In Listing 12-4, the char array firstname at Line 5 can hold 15 characters, plus 1 for the \0 at the end of the string. This 15-character limitation is an assumption made by the programmer; most first names are fewer than 15 characters long.

### LISTING 12-4: Filling a char Array

```
#include <stdio.h>

int main()
{
    char firstname[16];

    printf("What is your name? ");
    fgets(firstname,16,stdin);
    printf("Pleased to meet you, %s\n",firstname);
    return(0);
}
```

An fgets() function in Line 8 reads in data for the firstname string. The maximum input size is set to 16 characters, which already accounts for the null character because fgets() is smart that way. The text is read from stdin (the function's third argument), or standard input.

## Exercise 12-9: Create a new program using the source code from Listing 12-4. Build and run, using your first name as input.

Try running the program again, but fill up the buffer: Type more than 15 characters. You'll see that only the first 15 characters are stored in the array. Even the Enter key press isn't stored, which it would be otherwise when input is fewer than 15 characters.

## Exercise 12-10: Modify your source code from Exercise 12-9 so that the program also asks for your last name, storing this data in another array. The program should then greet you by using both your first and last names.

Yes, the Enter key press is stored as part of your name when you type fewer than 15 characters. This effect is how input is read by the fgets() function. If your first name is Dan, the array looks like this:

![](img/dcc0cd79d4a45cfce24fa49d85442884_195_0.png)

```
firstname[0] == 'D'
firstname[1] == 'a'
firstname[2] == 'n'
firstname[3] == '\n'
firstname[4] == '\0'
```

The newline lurks in the string because input in C is stream oriented and Enter is part of the input stream as far as the fgets() function is concerned. You can fix this issue by obeying Exercise 12-11.

## Exercise 12-11: Rewrite your source code from Exercise 12-10 so that the scanf() function is used to read in the first and last name strings.

Of course, the problem with the scanf() function is that it doesn't check to ensure that input is limited to 15 characters — that is, unless you direct it to do so:

## Exercise 12-12: Modify the scanf() functions in your source code from Exercise 12-11 so that the conversion character used is written as %15s. Build and run.

The %15s conversion character tells the first scanf() function to read only the first 15 characters of input and place it into the char array (string). Any extra text is then read by the second scanf() function, and any extra text after that is discarded.

![](img/dcc0cd79d4a45cfce24fa49d85442884_195_1.png)

It's critical that you understand stream input when it comes to reading text in C. Chapter 13 offers additional information on this important topic.

## Sorting arrays

Computers are designed to quickly and merrily accomplish boring tasks, such as sorting an array. In fact, they love doing it so much that "the sort" is a basic computer concept upon which many theories and algorithms have been written. It's a real snoozer topic if you're not a Mentat or a native of the planet Vulcan.

The simplest sort is the bubble sort, which not only is easy to explain and understand but also has a fun name. It also shows the basic array sorting philosophy, which is to swap values between two elements.

Suppose that you're sorting an array so that the smallest values are listed first. If array[2] contains the value 20, and array[3] contains the value 5, these two elements would need to swap values. To make it happen, you use a temporary variable that looks like this:

```
temp=array[2]; /* Save 20 in temp */
array[2]=array[3]; /* Store 5 in array[2] */
array[3]=temp; /* Put 20 in array[3] */
```

In a bubble sort, each array element is compared with every other array element in an organized sequence. When one value is larger (or smaller) than another, the values are swapped. Otherwise, the comparison continues, plodding through every possible permutation of comparisons in the array. Listing 12-5 demonstrates.

### A Bubble Sort

```
#include <stdio.h>
int main()
{
const int size = 6;
int bubble[] = { 95, 60, 6, 87, 50, 24 };
int inner,outer,temp,x;
/* Display Original array */
puts("Original Array:");
for(x=0;x<size;x++)
printf("%d\t",bubble[x]);
putchar('\n');
/* Bubble sort */
for(outer=0;outer<size-1;outer++)
```
