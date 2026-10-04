
```cpp
if (!isValidInt(value))
    cout << "The number you entered is not a valid integer.";
else{
    number = atoi(value.c_str());
    cout << "The integer you entered is " << number;
}

return 0;
}
```

```cpp
bool isValidInt(string str){
    int start = 0;
    int i;
    bool valid = true; // assume a valid
    bool sign = false; // assume no sign

    // check for an empty string
    if (int(str.length()) == 0) valid = false;

    // check for a leading sign
    if (str.at(0) == '-'||str.at(0) == '+')
        sign = true;
        start = 1; // start checking for digits after the sign

    // check that there is at least one character after the sign
    if (sign && int(str.length()) == 1) valid = false;

    // now check the string, which you know
    // has at least one non-sign character
    i = start;
    while(valid && i < int(str.length())){
        if(!isdigit(str.at(i))) valid = false; // found a non-digit character
        i++; // move to next character
    }

    return valid;
}
```

# Chapter 9 Input Data Validation 537

Two sample runs of Program 9.18 produced the following output:

```
Enter an integer: 12e45
The number you entered is not a valid integer.
```

and

```
Enter an integer: -12345
The integer you entered is -12345
```

As shown by this output, the program successfully determines that an invalid character was entered in the first run.

A second line of defense is to use error-processing code in the context of exception handling. This type of code is used to permit the user to correct a problem, such as invalid data entry, by entering a new value. The means of providing this code in C++ is referred to as exception handling.

Using exception handling, you can construct a complete means of ensuring that the user enters an integer instead of an invalid value. The technique involves extending isValidInt() function in Program 9.18 to ensure that not only is an invalid integer value detected, but also the program gives the user the option of reentering values until a valid double-precision number, which is the numerical data type requested-entered data.

Using the isValidInt from Program 9.18, a more comprehensive function named getInt() is developed that uses exception processing to accept user input continuously until a string corresponding to an integer is detected. After a string is entered, the getInt() function converts the string to an integer and returns the integer value. This technique ensures that the program requesting an integer actually receives an integer and prevents any unwarranted side effects, such as a program crash caused by an invalid data type being entered. The algorithm used to perform this task is as follows:

Set a Boolean variable named notantint to true (while notantint is true)

```text
try
  Accept a string value
  If the string value does not correspond to an integer, throw an exception
catch the exception
  Display the error message "Invalid integer - Please reenter:"
  Send control back to the while statement
  Set notantint to false (causes the loop to terminate)
end while
```

Return the integer corresponding to the entered string

The code corresponding to this algorithm is shown in Program 9.19.

# 538 Completing the Basics

# Program 9.19

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int getInt(); // function declaration (prototype)
    int value;

    cout << "Enter an integer value: ";
    value = getInt();
    cout << "The integer entered is: " << value << endl;

    return 0;
}

int getInt()
{
    bool isValidInt(string); // function declaration (prototype)
    bool notantint = true;
    string svalue;

    while (notantint)
    {
        try {
            cin >> svalue; // accept a string input
            if (!isValidInt(svalue)) throw svalue;
        }
        catch (string e)
        {
            cout << "Invalid integer - Please reenter: ";
            continue; // send control to the while statement
        }
        notantint = false;
    }
    return atoi(svalue.c_str()); // convert to an integer
}
```

# Chapter 9 Input Data Validation

```cpp
bool isValidInt(string str)
{
    int start = 0;
    int i;
    bool valid = true; // assume a valid
    bool sign = false; // assume no sign

    // check for an empty string
    if (str.length() == 0) valid = false;

    // check for a leading sign
    if (str.at(0) == '-' || str.at(0) == '+') {
        sign = true;
        start = 1; // start checking for digits after the sign
    }

    // check that there is at least one character after the sign
    if (sign && str.length() == 1) valid = false;

    // now check the string, which you know
    // has at least one non-sign character
    i = start;
    while (i < str.length()) {
        if (!isdigit(str.at(i))) valid = false; // found a non-digit character
        i++; // move to next character
    }

    return valid;
}
```

Following is a sample output produced by Program 9.19:

```
Enter an integer value: abc
Invalid integer - Please reenter: 12.
Invalid integer - Please reenter: 12e
Invalid integer - Please reenter: 120
The integer entered is: 120
```

As this output shows, the getInt() function works correctly. It requests input continuously until a valid integer is entered.

# EXERCISES 9.5

- 1. (Practice) Write a C++ program that prompts the user to type in an integer. Have your program use cin to accept the number as an integer and use cout to display the value your program accepted. Run your program four times. The first time you run, enter a valid integer; the second time, enter a double-precision number; the third time, enter a character; and the fourth time, enter the value -123.
- 2. (Modify) Modify the program you wrote for Exercise 1, but have your program use a double-precision number. Run the program four times: First, enter an integer; second, enter a decimal number; third, a decimal number with f as the last character; and fourth, enter a character. Using the output display, keep track of what happened, if anything, and why?
- 3. (For Thought) Why do you think successful applications contain extensive data checks? (Hint: Exercises 1 and 2.)
- b. What is the difference between a data-type check and a reasonableness check?
- c. A program requests the user to enter a month, day, and year. What are some reasonableness checks that could be made on the data entered?
- 4. (Practice) Enter and execute Program 9.18.
- b. Run Program 9.18 four times, using the data referred in Exercise 1 for each run.
- 5. (Modify) Modify Program 9.18 to display all invalid characters that were entered.
- 6. (Modify) Modify Program 9.18 to request an integer continuously until a valid number is entered.
- 7. (Modify) Modify Program 9.18 to remove all leading and trailing spaces from the entered string before it is checked for validity.
- 8. (Useful Utility) Write a function that checks each digit as it enters instead of the completed string, as in Program 9.18.
- 9. (Practice) Enter and execute Program 9.19.
- 10. (Modify) Modify the isValidInt() function used in Program 9.19 to remove all leading and trailing spaces from its string argument before determining the string corresponds to a valid integer.
- 11. (Modify) Modify the isValidInt() function used in Program 9.19 to accept a string that ends in a decimal point. For example, the input 12.0 should be accepted and converted to the integer number 12.

# A Closerer Look: Namespaces and Creating a Personal Library

# 9.6 A Closer Look: Namespaces and Creating a Library

Until the introduction of PCs in the early 1980s, with their extensive use of integrated circuits and microprocessors, computer speed and available memory were severely restricted. For example, the most advanced computers had speeds measured in milliseconds; current computers have speeds measured in nanoseconds and hardware of desktop computers consisted of 4000 bytes of internal memory; however, today's computer memories are in the 512 MB range and higher.

With these early hardware restrictions, programmers had to use every possible trick to save memory and make programs run more efficiently. Almost every program was hand-crafted and what was called "clever" to minimize runtime and maximize use of storage. Unfortunately, this individualized code became a liability. Programmers had to spend so time debugging code that the original programmer had trouble figuring out code written only months before. This complexity made modifications costly and precluded cost-effective reuse of existing code.

The inability to reuse code efficiently, combined with expanded hardware capabilities, prompted the discovery of more efficient programming. This discovery began with structuring concepts incorporated into procedural languages, such as Pascal, and led to the object-oriented techniques that form the basis of C++. An early criticism of C++, that there wasn't a comprehensive library of classes, but with the ANSI/ISO standard, an extensive C++ library is available.

No matter how useful classes and the standard library provides, however, each type of programming, such as engineering, scientific, and financial, has its own specialized requirements. For example, the time header in C++ provides good date and time functions. However, for specialized needs such as scheduling problems, functions must be expanded to include the number of working days between two dates, taking into account weekends and holidays, among other tasks. These functions could be provided as part of a more complete class or as non-class functions.

To meet these specialized needs, programmers create and share their own libraries of classes and functions with other programmers on the same or similar projects. After the classes and functions have been tested, they can be incorporated into any program without further coding time.

At this stage in your programming career, you can begin building your own library of specialized functions and classes. Section 9.5 will describe how to do this with the input functions, isValidInt() and getInt(), which are reproduced here for convenience:

```cpp
bool isValidInt(string string)
{
    int start = 0;
    int i;
    bool valid = true; // assume a valid
    bool sign = false; // assume no sign

    // check for an empty string
    if (int(str.length()) == 0) valid = false;
```
