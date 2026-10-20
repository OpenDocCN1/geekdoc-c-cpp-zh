
## C++ Input/Output

![](img/2f9c26fcf758b5bc56897d9c75b6347f_113_0.png)

There’s a satisfying feeling when you program code that asks the user for input, then uses that input to produce something that the user can see. Even if it’s simply asking for someone’s name, and displaying a personal welcome message, it’s a big leap forward.

User interaction, character literals, defining constants and file input and output are all covered in the following pages. All of which help you to understand how a C++ program works better.

- 116 User Interaction
- 118 Character Literals
- 120 Defining Constants
- 122 File Input/Output

## User Interaction

There’s nothing quite as satisfying as creating a program that responds to you. This basic user interaction is one of the most taught aspects of any language and with it you’re able to do much more than simply greet the user by name.

### HELLO, DAVE

You have already used cout, the standard output stream, throughout our code. Now you’re going to be using cin, the standard input stream, to prompt a user response.

### STEP 1

Anything that you want the user to input into the program needs to be stored somewhere in the system memory, so it can be retrieved and used. Therefore, any input must first be declared as a variable, so it’s ready to be used by the user. Start by creating a blank C++ file with headers.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_115_0.png)

### STEP 2

The data type of the variable must also match the type of input you want from the user. For example, to ask a user their age, you would use an integer like this:

```
#include <iostream>
using namespace std;

int main ()
{
    int age;
    cout << "what is your age: ";
    cin >> age;

    cout <<"\nYou are " << age << " years old.\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_115_1.png)

### STEP 3

The cin command works in the opposite way from the cout command. With the first cout line you’re outputting ‘What is your age’ to the screen, as indicated with the chevrons. Cin uses opposite facing chevrons, indicating an input. The input is put into the integer age and called up in the second cout command. Build and run the code.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_115_2.png)

### STEP 4

If you’re asking a question, you need to store the input as a string; to ask the user their name, you would use:

```
#include <iostream>
using namespace std;

int main ()
{
    string name;
    cout << "what is your name: ";
    cin >> name;

    cout << "\nHello, " << name << " . I hope you’re well today?\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_115_3.png)

### STEP 5

The principal works the same as the previous code. The user's input, their name, is stored in a string, because it contains multiple characters, and retrieved in the second cout line. As long as the variable 'name' doesn't change, then you can recall it wherever you like in your code

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_0.png)

### STEP 6

You can chain input requests to the user but just make sure you have a valid variable to store the input to begin with. Let's assume you want the user to enter two whole numbers:

```
#include <iostream>
using namespace std;

int main ()
{
    int num1, num2;

    cout << "Enter two whole numbers: ";
    cin >> num1 >> num2;

    cout << "you entered " << num1 << " and " << num2 << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_1.png)

### STEP 7

Likewise, inputted data can be manipulated once you have it stored in a variable. For instance, ask the user for two numbers and do some maths on them:

```
#include <iostream>
using namespace std;

int main ()
{
    float num1, num2;

    cout << "Enter two numbers: \n";
    cin >> num1 >> num2;

    cout << num1 << " + " << num2 << " is: " << num1 + num2 << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_2.png)

### STEP 8

While cin works well for most input tasks, it does have a limitation. Cin always considers spaces as a terminator, so it's designed for just single words not multiple words. However, getline takes cin as the first argument and the variable as the second:

```
#include <iostream>
using namespace std;

int main ()
{
    string mystr;
    cout << "Enter a sentence: \n";
    getline(cin, mystr);

    cout << "Your sentence is: " << mystr.size() << " characters long.\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_3.png)

### STEP 9

Build and execute the code, then enter a sentence with spaces. When you're done the code reads the number of characters. If you remove the getline line and replace it with cin >> mystr and try again, the result displays the number of characters up to the first space.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_4.png)

### STEP 10

Getline is usually a command that new C++ programmers forget to include. The terminating white space is annoying when you can't figure out why your code isn't working. In short, it's best to use getline(cin, variable) in future:

```
#include <iostream>
using namespace std;

int main ()
{
    string name;
    cout << "Enter your full name: \n";
    getline(cin, name);

    cout << "\nHello, " << name << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_5.png)

## Character Literals

In C++ a literal is an object or variable that once defined remains the same throughout the code. However, a character literal is defined by a backslash, such as the \n you've been using at the end of a cout statement to signify a new line.

When used in something like a cout statement, character literals are also called Escape Sequence Codes. They allow you to insert a quote, an alert, new line and much more.

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
}
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_117_0.png)

You've already experienced the \n character literal placing a new line wherever it's placed. The line: cout << "Hello\n" << "I'm a C++\n" << "Program!\n"; outputs three lines of text, each starting after the last \n.

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
	cout << "Hello\n" << "I'm a C++\n" << "Program!\n";
}
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_117_1.png)

If you wanted to insert speech quotes inside a cout statement, you would have to use a backslash as it already uses quotes:

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
	cout << "Hello, user. This is how to use \"quotes\".";
}
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_117_2.png)

There's even a character literal that can trigger an alarm. In Windows 10, it's the notification sound that chimes when you use \a. Try this code, and turn up your sound.

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
	cout << "ALARM! \a";
}
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_117_3.png)

### A HANDY CHART

There are numerous character literals, or escape sequence codes, to choose from. We therefore thought it would be good for you to have a handy chart available, for those times when you need to insert a code.

| ESCAPE SEQUENCE CODE | CHARACTER |
|---|---|
| \\ | Backslash |
| \' | Single Quote |
| \" | Double Quote (Speech Marks) |
| \? | Question Mark |
| \a | Alert/Alarm |
| \b | Backspace |
| \f | Form Feed |
| \n | New Line |
| \r | Carriage Return |
| \t | Horizontal Tab |
| \v | Vertical Tab |
| \0 | Null Character |
| \uxxxx | Unicode (UTF-8) |
| \Uxxxxxxxx | Unicode (UTF-16) |

### UNICODE CHARACTERS (UTF-8)

Unicode characters are symbols or characters that are standard across all platforms. For example, the copyright symbol, that can be entered via the keyboard by entering the Unicode code, followed by ALT+X. In the case of the copyright symbol enter: 00A9 Alt+X. In C++ code, you would enter:

```
#include <iostream>
using namespace std;

int main ()
{
    cout << "\u00A9";
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_118_0.png)

### UNICODE CHARACTER TABLE

A complete list of the available Unicode characters can be found at www.unicode-table.com/en/. Hover your mouse over the character to see its unique code to enter in C++.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_118_1.png)
