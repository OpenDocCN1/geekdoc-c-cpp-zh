# 220 Introduction to C++

Notice the return type of get() should be stored into an int variable, not char. See why. Suppose that char is declared as char. the char type is signed and the character with value 255 is, it will be stored as -1 into char. As a result, the condition which tests that value EOF becomes false and the loop stops reading more readers. If the char type is unsigned and get() returns EOF, you won't be stored as -1; the loop will terminate.

In case you where we do not read characters with cin in the same way we read numeric values, the reason is that white characters (e.g., spaces, tabs) are skipped by default. For example:

```
#include <iostream> // Example 9.3
int main()
{
    std::cout << "Enter character: ";
    std::cin >> ch;
    if(ch == ' ')
        std::cout << (int)ch;
    return 0;
}
```

Since the characters are skipped, if the user enters a space and presses Enter, the program neither displays something nor it terminates. To terminate, you must enter a non-white character. This behavior can change using the noskipws manipulator. That is, if we:

cin >> noskipws >> ch;

the white characters are not ignored. So, if the user enters a space the program displays the ASCII value of the space (i.e., 32) and in the general case the program is continuously reading characters until the user enters a specific character I prefer get(), because it does not skip the character (e.g., the program may require to count all the characters) and it is also easy to check with the EOF, the validity of the character.

An unexpected behaviour that makes many novice programmers wonder why their program is not working properly and make them crazy enough to crash the computer occurs when reading characters after reading numeric values. The following program is an example. Do you notice malfunction in the program when the user enters an integer and presses Enter?

```
#include <iostream> // Example 9.4
using std::cout;
using std::cin;
int main()
{
    int i, ch;

    cout << "Enter number: ";
    cin >> i;

    cout << "Enter character: ";
    ch = cin.get();
    cout << i << ' ' << (char)ch << '\n';
    return 0;
}
```

In case the user enters an integer and presses Enter, the generated new line character is stored in the input queue. get() gets it from there and stores it into the ch variable, without leaving the user type