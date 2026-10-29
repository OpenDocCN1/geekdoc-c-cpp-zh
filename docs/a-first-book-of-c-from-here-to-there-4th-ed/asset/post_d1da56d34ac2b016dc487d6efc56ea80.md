
Program 15.3 also shows a useful technique for developing functions. The shaded statements constitute a self-contained unit for entering a complete line of characters from the keyboard. These statements can be removed from main() and placed together as a new function.

In Program 15.4, the shaded statements from Program 15.3 are placed in a separate function named getaline(). Notice that in the process, the MAXCHARS constant has been placed above the main() function. This placement gives the constant a global scope, which makes it available to both the main() and getaline() functions.

## Program 15.4

```
#include <iostream>
using namespace std;

const int MAXCHARS = 81;   // global symbolic constant
void getaline(char []);    // function prototype

int main()
{
    char message[MAXCHARS]; // enough storage for a complete line

    cout << "Enter a sentence:\n";
    getaline(message);
    cout << "The sentence just entered is:\n";
    cout << message << endl;
}

void getaline(char strng[])
{
    int i = 0;
    char c;
    while(i < MAXCHARS && (c = cin.get()) != '\n')
    {
        strng[i] = c;   // store the character entered
        i++;
    }
    strng[i] = '\0';   // terminate the string

    return;
}
```

## EXERCISES 15.1

- 1. **(Program)** a. The following function can be used to select and display all vowels in a user-entered string:

```
void vowels(char strng[])
{
    int i = 0;
    char c;
    while ((c = strng[i++]) != '\0')
        switch(c)
        {
            case 'a':
            case 'e':
            case 'i':
            case 'o':
            case 'u':
                cout << c;
        } // end of switch
    cout << endl;
    return;
}
```

Note that the switch statement in vowels() uses the fact that selected cases “drop through” in the absence of break statements. Therefore, all selected cases result in a cout object call. Include vowels() in a working program that accepts a user-entered string and then displays all vowels in the string. In response to the input How much is the little now worth?, your program should display ouieieao.

b. Modify vowels() to count and display the total number of vowels in the string passed to it.

- 2. **(Modify)** Modify the vowels() function in Exercise 1a to count and display the numbers of each vowel in the string.

- 3. **(Program)** a. Write a C++ function to count the total number of characters, including blanks, in a string. Don’t include the end-of-string marker in the count.
  
  b. Include the function written for Exercise 3a in a complete working program.

- 4. **(Program)** Write a program that accepts a string of characters from the keyboard and displays the hexadecimal equivalent of each character.

- 5. **(Program)** Write a C++ program that accepts a string of characters from the keyboard and displays the string with one word per line.

- 6. **(Program)** Write a function that reverses the characters in a string. *(Hint: It can be considered a string copy, starting from the back end of the first string.)*

- 7. **(Program)** Write a function called `delChar()` that can be used to delete characters from a string. The function should take three arguments: the string name, the number of characters to delete, and the starting position in the string where characters should be deleted. For example, the call `delChar(string,13,5)`, when applied to the string `all enthusiastic people`, should result in the string `all people`.

- 8. **(Program)** Write a function called `addChar()` to insert one string of characters into another string. The function should take three arguments: the string to be inserted, the original string, and the position in the original string where the insertion should begin. For example, the call `addChar("for all",message,6)` should insert the characters `for all` in `message`, starting at `message[5]`.

- 9. **(Program)** a. Write a C++ function named `toUpper()` that converts lowercase letters to uppercase letters. The expression `c - 'a' + 'A'` can be used to make the conversion for any lowercase character stored in `c`.
  
  b. Add a data input check to the function written in Exercise 9a to verify that a valid lowercase letter is passed to the function. A character in ASCII is lowercase if it's greater than or equal to a blank and less than or equal to `z`. If the character isn't a valid lowercase letter, have the `toUpper()` function return the passed character unaltered.
  
  c. Write a C++ program that accepts a string from the keyboard and converts all lowercase letters in the string to uppercase letters.

- 10. **(Program)** Write a C++ program that accepts a string from the keyboard and converts all uppercase letters in the string to lowercase letters.

- 11. **(Program)** Write a C++ program that counts the number of words in a string. A word is encountered whenever there's a transition from a blank space to a nonblank character. Assume the string contains only words separated by blank spaces.

## 15.2 Pointers and C-String Library Functions

Pointers are exceptionally useful in constructing functions that manipulate C-strings. When pointer notation is used in place of subscripts to access characters in a C-string, the resulting statements are more compact and more efficient. This section describes the equivalence between subscripts and pointers when accessing characters in a C-string.

Take another look at the strcpy() function introduced in Section 15.1. It was used to copy the characters of one C-string to a second C-string. For convenience, this function is repeated here:

```
// a function to copy string2 to string1
void strcpy(char string1[], char string2[])
{
    int i = 0;

    while (string2[i] != '\0')    // check for end of string
    {
        string1[i] = string2[i];    // copy the element to string1
        i++;
    }
    string1[i] = '\0';            // terminate the first string

    return;
}
```

Before you see how to write a pointer version of strcpy(), two modifications should be made to the function to make it more efficient. The first modification has to do with the expression in the function's while statement. As written, it tests each character to ensure that the end of the C-string hasn't been reached. Like all relational expressions, the tested expression, string2[i] != '\0', is true or false. Take the string this is a string shown in Figure 15.3 as an example. As long as string2[i] doesn't access the end-of-C-string character, the expression's value is non-zero and considered to be true. The expression is false only when the expression's value is zero, which occurs when the last element in the C-string is accessed.

Recall that C++ defines false as zero and true as anything else. Therefore, the expression string2[i] != '\0' becomes zero (false) when the end of the string is reached. It's non-zero (true) everywhere else. The NULL character has an internal value of zero, so the comparison with '\0' isn't necessary. When string2[i] accesses the end-of-C-string character, the value of string2[i] is zero. When string2[i] accesses any other character, the value of string2[i] is the value of the code used to store the character and is non-zero. Figure 15.4 lists the ASCII codes for the string this is a string. As the figure shows, each element has a non-zero value except the NULL character.

| Element | String array | Expression | Value |
|---|---|---|---|
| Zeroth element | t | string2[0] != '\0' | 1 |
| First element | h | string2[1] != '\0' | 1 |
| Second element | i | string2[2] != '\0' | 1 |
|  | s |  |  |
|  |  |  |  |
|  | i |  |  |
|  | s |  |  |
| . |  | . | . |
| . | a | . | . |
| . |  | . | . |
|  | s |  |  |
|  | t |  |  |
|  | r |  |  |
|  | i |  |  |
|  | n |  |  |
| Fifteenth element | g | string2[15] != '\0' | 1 |
| Sixteenth element | \0 | string2[16] != '\0' | 0 |
| End-of-string marker |  |  |  |

Figure 15.3 The while test becomes false at the end of the string
