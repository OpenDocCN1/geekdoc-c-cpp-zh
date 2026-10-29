
# Point of Information

## Allocating Space for a String

Although both the following declarations

```
char test[5] = "abcd";
char *test = "abcd";
```

create storage for the characters 'a', 'b', 'c', 'd', and '\0', there's a subtle difference between the two declarations and in how values can be assigned to test. An array declaration, such as char test[5];, precludes subsequent use of an assignment expression, such as test = "efgh", to assign values to the array. Using the strcpy() function, as in strcpy(test, "efgh"), however, is valid. The only restriction on strcpy() is the array size, which in this case is five elements. This situation is reversed when a pointer is created. A pointer declaration, such as char *test;, precludes using strcpy() to initialize the memory locations pointed to by the pointer, but it does allow assignments. For example, the following sequence of statements is valid:

```
char *test;
test = "abcd";
test = "here is a longer string";
```

The difference in use is explained by the fact that the compiler automatically allocates enough new memory space for any C-string pointed to by a pointer variable but doesn't do so for an array of characters. The array size is fixed by the definition statement.

Formally, any expression yielding a value that can be used on the left side of an assignment expression is said to be an lvalue. (Similarly, any expression yielding a value that can be used on the right side of an assignment statement is said to be an rvalue.) Therefore, a pointer variable can be an lvalue, but an array name can't.

![](img/e9bf940282dfb289356f077151cc69dd_713_0.png)

Figure 15.7 The addresses in the seasons[] pointers

The initialization of the seasons array can also be incorporated into the definition of the array, as follows:

```
char *seasons[4] = {"Winter",
    "Spring",
    "Summer",
    "Fall"};
```

This declaration both creates an array of pointers and initializes the pointers with appropriate addresses. After addresses have been assigned to the pointers, each pointer can be used to access its corresponding string. Program 15.8 uses the seasons array to display each season by using a for loop.

## Program 15.8

```
#include <iostream>
using namespace std;
int main()
{
    const int NUMSEASONS = 4;
    int n;
    char *seasons[] = {"Winter",
        "Spring",
        "Summer",
        "Fall"};

    for( n = 0; n < NUMSEASONS; n++)
        cout << "\n\tThe season is " << seasons[n];

    return 0;
}
```

The output of Program 15.8 is as follows:

```
The season is Winter
The season is Spring
The season is Summer
The season is Fall
```

The advantage of using a list of pointers is that logical groups of data headings can be collected and accessed with one array name. For example, the months in a year can be grouped in one array called months, and the days in a week can be grouped in an array called days. The grouping of like headings enables the programmer to access and print a corresponding heading simply by specifying the heading's correct position in the array. Program 15.9 uses the seasons array to identify and display the season corresponding to a user-entered month.

## Program 15.9

```
#include <iostream>
using namespace std;
int main()
{
    int n;
    char *seasons[] = {"Winter",
                        "Spring",
                        "Summer",
                        "Fall"};

    cout << "\nEnter a month (use 1 for Jan., 2 for Feb., etc.): ";
    cin >> n;
    n = (n % 12) / 3;  // create the correct subscript
    cout << "The month entered is a " << seasons[n] << " month.";

    return 0;
}
```

Except for the expression n = (n % 12) / 3, Program 15.9 is rather straightforward. The program requests the user to enter a month and accepts the number corresponding to the month, using a cin object to display the selected month. The expression n = (n % 12) / 3 uses a common programming "trick" to scale a set of numbers into a more useful set. Using subscripts, the four elements of the seasons array must be accessed via a subscript from 0 through 3. Therefore, the months of the year, which correspond to the numbers 1 through 12, must be adjusted to correspond to the correct season subscript by using the expression n = (n % 12) / 3. The expression n % 12 adjusts the user-entered month to lie in the range 0 through 11, with 0 corresponding to December, 1 to January, and so on. Dividing by 3 causes the resulting number to range between 0 and 3, corresponding to the possible seasons elements. The result of the division by 3 is assigned to the integer variable n. The months 0, 1, and 2, when divided by 3, are set to 0; the months 3, 4, and 5 are set to 1; the months 6, 7, and 8 are set to 2; and the months 9, 10, and 11 are set to 3. It's equivalent to the following assignments:

| Months | Season |
|---|---|
| December, January, February | Winter |
| March, April, May | Spring |
| June, July, August | Summer |
| September, October, November | Fall |

The following is a sample output from Program 15.9:

```
Enter a month (use 1 for Jan., 2 for Feb., etc.): 12
The month entered is a Winter month.
```

## EXERCISES 15.3

- 1. (Practice) Write two declaration statements that can be used in place of the declaration char text[] = "Hooray!";

- 2. (Desk check) Determine the value of *text, *(text + 3), and *(text + 7) for each of the following sections of code:
  - a. char *text;
    char message[] = "the check is in the mail";
    text = message;
  - b. char *text;
    char formal[] = {'T','h','i','s',' ','i','s',' ','a','n',' ',
    'i','n','v','i','t','a','t','i','o','n','\0'};
    text = &formal[0];
  - c. char *text;
    char more[] = "Happy Holidays";
    text = &more[4];
  - d. char *text, *second;
    char blip[] = "The good ship";
    second = blip;
    text = ++second;

- 3. (Debug) Determine the error in the following program:

```
#include <iostream>
using namespace std;
int main()
{
    int i = 0;
    char message[] = {'H','e','l','l','o','\0'};
    for( ; i < 5; i++)
    {
        cout << *message;
        message++;
    }
    return 0;
}
```

- 4. (Program) a. Write a C++ function that displays the day of the week corresponding to a user-entered number between 1 and 7. That is, in response to the input 2, the program displays the name Monday. Use an array of pointers in the function.
  - b. Include the function written for Exercise 4a in a complete working program.

5. (Modify) Modify the function written in Exercise 4a so that it returns the address of the character string containing the correct day to be displayed.

6. (Program) Write a function that accepts 10 lines of user-entered text and stores them as 10 C-strings. Use a pointer array in your function.

## 15.4 Common Programming Errors

The following errors are frequently made when pointers to C-strings are used:

- 1. Using the pointer to "point to" a nonexistent data element. This error is, of course, the same error you have already seen when using subscripts. C++ compilers don't perform bounds checking on arrays, so it's the programmer's responsibility to ensure that the address in the pointer is the address of a valid data element.

- 2. Not providing enough space for the C-string to be stored. A simple variation of this error is not providing space for the end-of-string NULL character when a C-string is defined as an array of characters and not including the '\0' character when the array is initialized. A more complicated variation of this error is declaring a character pointer, such as char *p; and then attempting to copy a C-string with a statement such as strcpy(p, "Hello");. Because no space has been allocated for the C-string, the C-string overwrites the memory area pointed to by p.

- 3. Misunderstanding the terminology. For example, if message is defined as
  char *message;
  the variable message is sometimes referred to as a string. Therefore, you might see wording such as "Store the characters Hooray for the Hoosiers in the string named message." Strictly speaking, calling message a string or a C-string variable is incorrect. It's a pointer containing the address of the first character in a C-string. Nevertheless, referring to a character pointer as a C-string occurs often enough that you should be aware of it.

## 15.5 Chapter Summary

- 1. A C-string is an array of characters terminated by the NULL character, '\0'.

- 2. C-strings can always be processed with standard array-processing techniques. Entering and displaying a C-string, however, always require relying on standard library functions.

- 3. The cin object and the cin.get() and cin.getline() functions can be used to input a C-string. The cin object tends to be of limited usefulness for C-string input because it terminates input when encountering a blank.

- 4. The cout object can be used to display C-strings.

- 5. In place of subscripts, pointer notation and pointer arithmetic are especially useful for manipulating C-string elements.
