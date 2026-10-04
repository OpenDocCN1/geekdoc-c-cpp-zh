# Problem Solving Using C++

# The cout Object

One of the most versatile and commonly used output, is an object named cout (pronounced “see out” and derived from console output). It's an output object that sends data it receives to the standard display device. For most systems, this display is a computer screen. For example, if the data Hello there! is sent to cout, this data is displayed on your screen. To send the data Hello world! to cout, enclose the text in quotation marks (“text in here”) and place the insertion symbol, <<, after the object's name and before the message, as shown in this line:

```
cout << "Hello there world!";
```

Now you see how to put all this together into a working C++ program, Program 2.1, that can run on your computer.

![](bbox=[0.107, 0.358, 0.175, 0.398])

# Program 2.1

```
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello there world!";

    return 0;
}
```

The first line of the program is a preprocessor command that uses the reserved word include:

#include <iostream>

Preprocessor commands begin with a pound sign (#) and perform some action before the compiler translates the source program into machine code. Specifically, the #include preprocessor command carries the contents of the file—in this case, iostream—to be inserted where needed. The iostream file is part of the standard library that contains, among other code, two classes: istream and ostream provide data declarations and methods for data input and output, respectively. The iostream file is called a header file because a reference to it is always placed at the top, or head, of a C++ program by using the #include command. You might be wondering what it has to do with this simple program. The answer is that the cout object is created from the ostream class. Therefore, the iostream header file must be included in all programs using cout. As shown in Program 2.1, preprocessor commands do not end with a semicolon.