
## Counting Loops

Remember that in Python a loop doesn’t count the last number you specify in a range. So if you wanted the loop to count from 1 to 10, then you will need to use:

```python
n = list(range(1, 11))
```

Which will return 1 to 10.

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_70_0.png)

## Case Sensitive

Python is a case sensitive programming language, so you will need to check any variables you assign. For example, `Lives=10` is a different variable to `lives=10`, calling the wrong variable in your code can have unexpected results.

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_70_1.png)

## Brackets

Everyone forgets to include that extra bracket they should have added to the end of the statement. Python relies on the routine having an equal amount of closed brackets to open brackets, so any errors in your code could be due to you forgetting to count your brackets; including square brackets.

```python
def print_game_status(self):
    print (board[len(self.missed_letters)])
    print ('Word: ' + self.hide_word())
    print ('Letters Missed: ',)
    for letter in self.missed_letters:
        print (letter,)
    print ()
    print ('Letters Guessed: ',)
    for letter in self.guessed_letters:
        print (letter,)
    print ()
```

## Colons

It’s common for beginners to forget to add a colon to the end of a structural statement, such as:

```
class Hangman:
def guess(self, letter):
```

And so on. The colon is what separates the code, and creates the indents to which the following code belongs to.

```python
class Hangman:
    def __init__(self,word):
        self.word = word
        self.missed_letters = []
        self.guessed_letters = []

    def guess(self,letter):
        if letter in self.word and letter not in self.guessed_letters:
            self.guessed_letters.append(letter)
        elif letter not in self.word and letter not in self.missed_letters:
            self.missed_letters.append(letter)
        else:
            return False
        return True

    def hangman_over(self):
        return self.hangman_won() or (len(self.missed_letters) == 6)

    def hangman_won(self):
        if '_' not in self.hide_word():
            return True
        return False

    def hide_word(self):
        rtn = ''
        for letter in self.word:
            if letter not in self.guessed_letters:
                rtn += '_'
            else:
                rtn += letter
        return rtn
```

## Operators

Using the wrong operator is also a common mistake to make. When you’re performing a comparison between two values, for example, you need to use the equality operator (a double equals, `==`). Using a single equal (`=`) is an assignment operator that places a value to a variable (such as, `lives=10`).

```python
b = 5
c = 10
d = 10
b == c #false because 5 is not equal to 10
c == d #true because 10 is equal to 10
```

## Operating Systems

Writing code for multiple platforms is difficult, especially when you start to utilise the external commands of the operating system. For example, if your code calls for the screen to be cleared, then for Windows you would use `cls`. Whereas, for Linux you need to use `clear`. You need to solve this by capturing the error and issuing it with an alternative command.

```python
# Code to detect error for using a different OS
run=1
while(run==1):
    try:
        os.system('clear')
    except OSError:
        os.system('cls')
    print('\n>>>>>>>>>>Python 3 File Manager<<<<<<<<<<\n')
```

## Beginner C++ Mistakes

There are many pitfalls the C++ developer can encounter, especially as this is a more complex and often unforgiving language to master. Beginners need to take C++ a step at a time and digest what they’ve learned before moving on.

### Common C++ Mistakes

Admittedly it’s not just C++ beginners that make the kinds of errors we outline on these pages, even hardened coders are prone to the odd mishap here and there. Here are some common issues to try and avoid.

### Undeclared Identifiers

A common C++ mistake, and to be honest a common mistake with most programming languages, is when you try and output a variable that doesn’t exist. Displaying the value of x on-screen is fine but not if you haven’t told the compiler what the value of x is to begin with.

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_71_0.png)

### Std Namespace

Referencing the Standard Library is common for beginners throughout their code, but if you miss the std:: element of a statement, your code errors out when compiling. You can combat this by adding:

```cpp
using namespace std;
```

Under the #include part and simply using cout, cin and so on from then on.

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_71_1.png)

### Semicolons

Remember that each line of a C++ program must end with a semicolon. If it doesn’t then the compiler treats the line with the missing semicolon as the same line with the next semicolon on. This creates all manner of problems when trying to compile, so don’t forget those semicolons.

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_71_2.png)

### GCC or G++

If you’re compiling in Linux then you will no doubt come across gcc and g++. In short, gcc is the GNU Compiler Collection (or GNU C Compiler as it used to be called) and g++ is the GNU C++ (the C++ version) of the compiler. If you’re compiling C++ then you need to use g++, as the incorrect compiler drivers will be used.

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_71_3.png)

### Comments (Again)

Indeed the mistake of never making any comments on code is back once more. As we’ve previously bemoaned, the lack of readable identifiers throughout the code makes it very difficult to look back at how it worked, for both you and someone else. Use more comments.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    vector<double> v;
    double d;
    while (cin >> d) v.push_back(d);    // read elements
    if (cin.eof()) {                    // check if input failed
        cerr << "format error\n";       // error return
        return 1;
    }

    cout << "read " << v.size() << " elements\n";
    reverse(v.begin(), v.end());
    cout << "elements in reverse order:\n";
    for (int i = 0; i < v.size(); ++i) cout << v[i] << '\n';

    return 0;                           // success return
}
```

### Quotes

Missing quotes is a common mistake to make, for every level of user. Remember that quotes need to encase strings and anything that’s going to be outputted to the screen or into a file, for example. Most compiler errors are due to missing quotes in the code.

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_72_0.png)

### Extra Semicolons

While it’s necessary to have a semicolon at the end of every C++ line, there are some exceptions to the rule. Semicolons need to be at the end of every complete statement but some lines of code aren’t complete statements. Such as:

```text
#include
if lines
switch lines
```

If it sounds confusing don’t worry, the compiler lets you know where you went wrong.

```cpp
// Program to print positive number entered by the user
// If user enters negative number, it is skipped

#include <iostream>
using namespace std;

int main()
{
    int number;
    cout << "Enter an integer: ";
    cin >> number;

    // checks if the number is positive
    if (number > 0)
    {
        cout << "You entered a positive integer: " << number << endl;
    }

    cout << "This statement is always executed.";
    return 0;
}
```

### Too Many Braces

The braces, or curly brackets, are beginning and ending markers around blocks of code. So for every `{` you must have a `}`. Often it’s easy to include or miss out one or the other facing brace when writing code; usually when writing in a text editor, as an IDE adds them for you.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int x;
    string mystring = "This is a string!\n";
    cout << "What's the value of x? ";
    cin >> x;
    cout << x;
    {
        cout << "\n\n";
        cout << mystring;
    }
}
```

### Initialise Variables

In C++ variables aren’t initialised to zero by default. This means if you create a variable called x then, potentially, it is given a random number from 0 to 18,446,744,073,709,551,616, which can be difficult to include in an equation. When creating a variable, give it the value of zero to begin with: x=0.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int x;
    x=0;

    cout << x;
}
```

### a.out

A common mistake when compiling in Linux is forgetting to name your C++ code post compiling. When you compile from the Terminal, you enter:

```bash
g++ code.cpp
```

This compiles the code in the file code.cpp and create an a.out file that can be executed with ./a.out. However, if you already have code in a.out then it’s overwritten. Use:

```bash
g++ code.cpp -o nameofprogram
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_72_1.png)
