
must be of the same data type as the array which is to be allocated dynamically.

The lifetime of a dynamically allocated variable may be as long as that of the program's execution. However, before the end of the program the pointer that points to a dynamically created variable goes out of scope, you no longer have any way of accessing the dynamically created memory. Therefore, the dynamically created variable still takes up memory, but is inaccessible. This is called a memory leak. To avoid memory leaks, you use the delete operator on the pointer that points to the dynamically allocated memory. This deallocates the dynamically allocated memory.

The return value of a function may be a pointer. If so, the pointer should point to either a static local variable or a dynamically created variable, not a local variable.

![](img/59a3417a6d5906fae6d8000d4c2cff76_227_0.png)

# Quiz

-1. What is a pointer?
2. Name a C++ task that requires a pointer to be performed.
3. What is the difference between declaring an integer variable and declaring an integer pointer variable?
4. What is the meaning of the data type in the declaration of a pointer?
5. What is the meaning and purpose of NULL?
6. What operator do you use to assign a pointer the address of another variable or constant?
7. What is the purpose of the indirection operator?
8. May a pointer point to different memory addresses at different times in the program?
9. May more than one pointer point to the same memory address?
10. What is the effect of incrementing a pointer variable?
11. What are the purposes of the new and delete operators?

# Chapter 12: Character, C-String, and C++ String Class Functions

# Overview

The word "character" has many meanings. A more complimentary definition is used to denote a person with good character. A less complimentary meaning, which I heard more than from my parents and teachers, that I was a character.

The word character has a third meaning in programming, though—as a data type. As you learned Chapter 2, each printable (letter, digit, punctuation) or whitespace (ENTER, TAB, SPACEBAR) key on the keyboard has a corresponding ANSI, ASCII, or Unicode value. Thus, you can assign any single input to a character variable without fear of a type mismatch.

Of course, a user's input may consist of more than one character. As you learned Chapter 10, individual characters may be organized together as a character array. Usually, a character array is ended by a null character, so its value can be output by the cout object and the stream insertion operator (<<). Such a null-terminated array is referred to as a "C-string". "C" in "C-string" refers to this character array being used in the C programming language, which was the predecessor to the C++ programming language.

C-strings are often used for data entry. For example, if the user is to enter a four-digit number, but enters "left", an attempt to assign that input directly to an integer variable will result in either a run-time error or the variable having a "garbage" value such as -5468. However, if the user input is assigned to a five-element array (the fifth element for the null character), no error would occur as any input can be represented as a character, and each character in the character array can be verified as a digit. If proper input is verified, then you can use standard library functions, as I will show you in this chapter, to convert the character representation of an integer, long, or float value into an actual integer, long, or float value.

The C++ programming language introduced the string data type, also referred to as the C+ string class. The C++ string class is often used instead of a C-string. The functions used by C-strings and the C++ string class, respectively, will be compared and contrasted in this chapter.

# Reading a Character

You may legitimately wonder why I am deviating this section of this chapter to reading a character. After all, reading a character is usually relatively simple. You just use the cin object and the stream insertion operator (>>) as in the following code fragment:

```
char grade;
cout << "Enter a grade: ";
cin >> grade;
```

However, in programming, as in life, matters are rarely as simple as they first appear to be, and this is no exception. The seemingly minor detail of the ENTER being pressed to end input gives rise to several interesting, and fortunately quite solvable, problems.

# The “Press Any Key to Continue” Problem

The preceding code fragment had the user enter a character which was assigned to a character variable. However, the process of user inputting a character is not always to assign that input to a variable.

For example, programs often prompt the user to press any key to continue. Indeed, a standard technical support joke concerns the user who complains that their keyboard does not have an "any" key. Of course, any key means any key on the keyboard, including the ENTER key.

While this may be entertaining, implementing the "press any key to continue" functionality to include the ENTER key is more complicated than first appears.

Let's examine the program:

```
#include <iostream>
using namespace std;

int main(void)
{
  char ch;
  do {
    cout << "Press Q or q to quit, any other key to continue:";

    cin >> ch;
    if (ch != 'Q' && ch != 'q')
      cout << "You want to continue\n";
    else
      cout << "You quit\n";
  } while (ch != 'Q' && ch != 'q');
  return 0;
}
```

The program works fine if you press Q or q to quit. The program also works fine if you press any other printable character to continue, such as a letter other than Q or q, a digit, or a punctuation mark.

However, if you press the ENTER key to? The answer is: nothing happens; cin is still waiting for you to enter. You have to enter a printable character to continue. The reason is that the stream extraction operator (>>) ignores all

whitespace characters, such as the newline character caused by pressing the ENTER key.

# The cin.get Function

Chapter 10, we discussed the getline function of the cin object. The getline function is a member function. A member function is not called by itself, as is, for example, the pow function we used in Chapter 4 to raise a number to a certain power. Instead, a member function is called from an object. Here, getline is a member function of cin. It is called from cin, and separated by a dot, as in cin.get(name, 80).

Here we use another member function of cin, the get member function is briefly explained in Chapter 10. The get, like the getline function, could be with two or three arguments, the first argument being a character array.

In addition to the two and three arguments, the get member function may also be called with no arguments or one argument. Unlike the three versions, the zero and one argument versions of the get member function are used to read a single character rather than a character array. The one-argument version will be discussed in this section. The no-argument version will be discussed in the next next section, titled "cin.ignore Function."

The data type of the one argument is a character, and the value of this argument changes to whichever keyboard key user pressed. This is true even if the ENTER key is pressed. ENTER then, the cin object with the stream insertion operator (<<), may be used to assign to a character variable the newline resulting from pressing the ENTER key.

We will make change to the previous program. We will change the statement cin >> ch to cin.get(ch), so the program now reads as:

```
#include <iostream>
using namespace std;

int main()
{
    char ch;
    do {
        cout << "Press Q or q to quit, any other key to continue:";
        cin.get(ch);
        if (ch == 'Q' && ch != 'q')
            cout << "You want to continue?\n";
        else
            cout << "You quit\n";
    } while (ch != 'Q' && ch != 'q');
    return 0;
}
```

Now, as the following input and output, the program works if you press the ENTER key to continue:

Press Q or q to quit, any other key to continue:
You want to continue?
Press Q or q to quit, any other key to continue: q
You quit
