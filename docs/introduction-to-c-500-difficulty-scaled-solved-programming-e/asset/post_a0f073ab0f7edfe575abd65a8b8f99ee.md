
## 40 Introduction to C++

When the cin statement is executed, the program waits for the user to enter a value. Usually, a cout statement precedes cin to indicate what kind of data to enter. Once the user enters integers and presses Enter, this value will be stored in i. Because the value is not stored before pressing Enter, the user can change it. For example, if the user enters the 5 and presses Enter, i will become 5. Then, the program waits for the user to enter a new value. For example, if the user enters 1.23 and presses Enter, j will become 1.23. Like cout, cin is a smart object. It converts input, which is a series of characters typed into the keyboard, into a format that fits the receiving data. For example, in case of i, it is converted to integer.

We cannot use the cin >> many times in the cin statement to enter multiple values. For example, we can write cin >> j;. In this case input values must be separated from each other by more or one space to distinguish. For example, if the user enters 5 and 1.23, i will become 5 and j will become 1.23. With the data written to cout, the data read from an input stream, as the characters, are stored in an intermediate memory. A C++ program flush this memory when Enter is pressed. Notice that if the user enters values that do not correspond to the types of variables, for example, two floats and an integer, incorrect values will be stored in i and j.

The operator skips any white characters (spaces, tabs, new lines) that may exist before the numeric value and continues until it encounters a non-white character. If it encounters a character that does not match the type of the variables, it is stripped away. The unread characters are left in cin. For example, if the user enters the values 5 and 1.23ABC, the ABC characters remain in cin and A will be the first character to be read with the next cin statement.

If we want to specify the numbering system of the integer to be read we can use the hex, oct, and dec manipulators. For example, we write:

```cpp
int i;
cout << "Enter number in hex: ";
cin >> i;
```

and the user enters f, i becomes 15.

For those who are unfamiliar with scanf() from C, you can also use it, but like printf(), it is complex, unsafe, and not scalable. Here is an example of a common error:

```cpp
int i;
scanf("%d", &i); /* Wrong, it should be instead of i. The code compiles successfully, however it won't run properly. */
```

My advice for those who would prefer to use printf()/scanf() as cout/cin, even if you know their peculiarities, it's time to stop using them. Put them in the drawer of your programming memories.

## Specific Input Format

Usually, a program asks the user to enter some values. However, there are cases where the user may be asked to enter the data in a specific format. For example, a program that requires the data to be entered in day/month/year format. One way to get the values we are interested in and assign them to corresponding variables is to use extra variable() to extract the characters we are not interested in. For example, the variable ch is used to extract the :

```cpp
char ch;
int d, m, y;
cout << "Enter date in the form d/m/y: ";
cin >> d >> ch >> m >> ch >> y;
```

In this example, the user must enter the date in the expected format (e.g., 13/5/2030), otherwise this code won't work.

## Check Input Stream Status

Without going into details, it is useful to know that you can check if the input data caused the cin statement to fail. One way is to use the member function good(). If no error occurs, it returns a non-zero value. If an error occurs you can use the clear() method to restore the stream's state. For example, the following program checks the return value of good() to ensure that an integer is stored into it. Do not be scared of the program, take a look at it, you will be able to understand it after learning the basics of the language.

```cpp
#include <iostream> // Example 3.8
#include <cstdio>
using std::cout;
using std::cin;
```

```cpp
int main()
{
    int ch, i;
    while (1) {
        cout << "Enter number: ";
        cin >> i;
        if(cin.good())
            break;
        cin.clear();
        while ((ch = cin.get()) != '\n' && ch != EOF)
            { // Clear the unload characters.
        }
    }
    cout << "Result: " << i << endl;
}
```For example, if the user enters the values 5 and 1.23ABC, the ABC characters remain in cin and A will be the first character to be read with the next cin statement.

If we want to specify the numbering system of the integer to be read we can use the hex, oct, and dec manipulators. For example, we write:

```cpp
int i;
cout << "Enter number in hex: ";
cin >> i;
```

and the user enters f, i becomes 15.

For those who are unfamiliar with scanf() from C, you can also use it, but like printf(), it is complex, unsafe, and not scalable. Here is an example of a common error:

(Note: The text contains some repetitions which were merged based on the logical flow.)

## EXERCISES

- 3.1 What is the output of the following program?
```cpp
#include <iostream>
using namespace std;
int main() {
    int i, j, k;
    cout << "Enter three numbers: ";
    cin >> i >> j >> k;
    cout << "Sum: " << i+j << endl;
    return 0;
}
```

- 3.2 What is the output of the following program?
```cpp
#include <iostream>
using namespace std;
int main() {
    int i, j;
    double d;
    cout << "Enter two numbers: ";
    cin >> i >> j;
    cout << "Result: " << i/j << endl;
    return 0;
}
```

- 3.3 What is the output of the following program?
```cpp
#include <iostream>
using namespace std;
int main() {
    int i, j;
    cout << "Enter two numbers: ";
    cin >> i >> j;
    cout << "Sum: " << (int)i+(int)j << endl;
    return 0;
}
```

- 3.4 What is the output of the following program?
```cpp
#include <iostream>
using namespace std;
int main() {
    int i, j, k;
    cout << "Enter three numbers: ";
    cin >> i >> j >> k;
    cout << "Sum: " << i+j+k << endl;
    return 0;
}
