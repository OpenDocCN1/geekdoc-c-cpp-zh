# 384 CHAPTER 9 Strings

# The Member Function get

The function can be used to read one character of input. Unlike the extraction operator, >> reads the next input character, no matter what character is. In particular, get will read a blank or the newline character, '\n', if either of these are the next input character. The function takes one argument, which should be a type of char. When called, the next input character is read and the argument variable has its value set equal to this input character.

# EXAMPLE

```
char nextSymbol;
cin.get(nextSymbol);
```

As we will see in Chapter 12, if you want to get from a file, you use an input-file stream in place of the stream cin.

If your program uses cin.get or cout.put, just as with other uses of cin and cout, your program should include one of the following (or something similar):

```
#include <iostream>
using namespace std;
```

or

```
#include <iostream>
using std::cin;
using std::cout;
```

# EXAMPLE: Checking Input Using a Newline Function

The function getInput in Display 9.2 asks the user if the input is correct and asks for a new value if the user says the input is incorrect. The program in Display 9.2 is just a driver program to test the function getInput, but the function, or one very similar to it, can be used in just any kind of program that takes input from the keyboard.

Notice the call to the function newline(). The function reads all the characters on the remainder of the line but does nothing with them. This amounts to discarding the remainder of the line. Thus, if the user types No, then the program reads the first letter, which is N, and then calls the function newline, which discards the rest of the input line. This means that if the user types 75 on the next input line, as shown in the sample dialogue, the program will read the number 75 and will not attempt to read the letter o in No. If the program did not include a call to the function newline, then the next item read would be the o in the line containing No instead of the 75 on the following line.