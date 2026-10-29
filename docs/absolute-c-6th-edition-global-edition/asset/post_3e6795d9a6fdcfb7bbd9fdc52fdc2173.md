
the output streams cout and cerr, which are in the class ostream. This chapter introduced the full output streams, which are in the class ofstream (with an 'f'). The class ostream is the class of all output streams. The streams cout and cerr are of type ostream, but not of type ofstream. In contrast to cout or cerr, an output-file stream is declared to be of type ofstream. The class ofstream of output-file streams is a derived class of the class ostream. For example, the following function writes the word "Hello" to the output stream given as its argument:

```
void sayHello(ostream& anyOutStream)
{
    anyOutStream << "Hello";
}
```

The first of the following calls writes "Hello" to the screen; the second writes "Hello" to the file with the external file name afile.txt:

```
ofstream fout;
fout.open("afile.txt");
sayHello(cout);
sayHello(fout);
```

Note that an output-file stream is of type ofstream and of type ostream. Derived classes are often discussed using the metaphor of inheritance and family relationships. If class D is a derived class of class B, then class D is called a child of class B and class B is called a parent of class D. The derived class is said to inherit the member functions of its parent class. For example, every convertible inherits the fact that it has four wheels from the class of all automobiles, and every input-file stream inherits the extraction operator, >>, from the class of all input streams. This is why the topic of derived classes is often called inheritance.

## EXAMPLE: Another newLine Function

As an example of how you can make a stream function more versatile, consider the function newLine that we defined in Display 9.2. That function works only for input from the keyboard, which is input from the predefined stream cin. The function newLine in Display 9.2 has no arguments. Next we have rewritten the function newLine so that it has a formal parameter of type istream for the input stream.

```
//Uses <iostream>;
void newLine(istream& inStream)
{
    char symbol;
    do
    {
        inStream.get(symbol);
    } while (symbol != '\n');
}
```

### EXAMPLE: (continued)

Now, suppose your program contains this new version of the function newline. If your program is taking input from an input stream called fin (which is connected to an input file), the following will discard all the input left on the line currently being read from the input file:

```
newLine(fin);
```

If your program is also reading some input from the keyboard, the following will discard the remainder of the input line that was typed in at the keyboard:

```
newLine(cin);
```

If your program has only the previous rewritten version of newLine, which takes a stream argument such as fin or cin, you must always give the stream name, even if the stream name is cin. But thanks to overloading, you can have both versions of the function newLine in the same program: the version with no arguments that is given in Display 9.2 and the version with one argument of type istream that we just defined. In a program with both definitions of newLine, the following two calls are equivalent:

```
newLine(cin);
```

and

```
newLine();
```

You do not really need two versions of the function newLine. The version with one argument of type istream can serve all your needs. However, many programmers find it convenient to have a version with no arguments for keyboard input, since keyboard input is used so frequently.

An alternative to having two overloaded versions of the newLine function is to use a default argument (as discussed in Chapter 4). In the following code, we have rewritten the newLine function a third time:

```
//Uses <iostream>
void newLine(istream& inStream = cin)
{
    char symbol;
    do
    {
        inStream.get(symbol);
    } while (symbol != '\n');
}
```

### EXAMPLE: (continued)

If we call this function as

```
newLine( );
```

the formal parameter takes the default argument cin. If we call this as

```
newLine(fin);
```

the formal parameter takes the argument fin.

An alternative to using this newLine function is to use the function ignore, which we discussed in Chapter 9. The function ignore is a member of every input file stream as well as a member of cin.

## Making Stream Parameters Versatile

If you want to define a function that takes an input stream as an argument and you want that argument to be cin in some cases and an input-file stream in other cases, then use a formal parameter of type istream (without an ‘f’). However, an input-file stream, even if used as an argument of type istream, must still be declared to be of type ifstream (with an ‘f’).

Similarly, if you want to define a function that takes an output stream as an argument and you want that argument to be cout in some cases and an output-file stream in other cases, then use a formal parameter of type ostream. However, an output-file stream, even if used as an argument of type ostream, must still be declared to be of type ofstream (with an ‘f’). You cannot open or close a stream parameter of type istream or ostream. Open these objects before passing them to your function and close them after the function call.

The stream classes istream and ostream are defined in the iostream library and placed in the std namespace. One way to make them available to your code is the following:

```
#include <iostream>
using std::istream;
using std::ostream;
```

## Self-Test Exercises

+   13. What is the type of the stream cin? What is the type of the stream cout?

+   14. Define a function called copyChar that takes one argument that is an input stream. When called, copyChar will read one character of input from the input stream given as its argument and will write that character to the screen. You should be able to call your function using either cin or an input-file stream as the argument to your function copyChar. (If the argument is an

(continued)

### Self-Test Exercises (continued)

input-file stream, then the stream is connected to a file before the function is called, so copyChar will not open or close any files.) For example, the first of the following two calls to copyChar will copy a character from the file stuff.txt to the screen, and the second will copy a character from the keyboard to the screen:

```
ifstream fin;
fin.open("stuff.txt");
copyChar(fin);
copyChar(cin);
```

+   15. Define a function called `copyLine` that takes one argument that is an input stream. When called, `copyLine` reads one line of input from the input stream given as its argument and writes that line to the screen. You should be able to call your function using either `cin` or an input-file stream as the argument to your function `copyLine`. (If the argument is an input-file stream, then the stream is connected to a file before the function is called, so `copyLine` will not open or close any files.) For example, the first of the following two calls to `copyLine` will copy a line from the file `stuff.txt` to the screen, and the second will copy a line from the keyboard to the screen:

```
ifstream fin;
fin.open("stuff.txt");
copyLine(fin);
copyLine(cin);
```

+   16. Define a function called `sendLine` that takes one argument that is an output stream. When called, `sendLine` reads one line of input from the keyboard and outputs the line to the output stream given as its argument. You should be able to call your function using either `cout` or an output-file stream as the argument to your function `sendLine`. (If the argument is an output-file stream, then the stream is connected to a file before the function is called, so `sendLine` will not open or close any files.) For example, the first of the following calls to `sendLine` will copy a line from the keyboard to the file morestuf.txt, and the second will copy a line from the keyboard to the screen:

```
ofstream fout;
fout.open("morestuf.txt");
cout << "Enter 2 lines of input:\n";
sendLine(fout);
sendLine(cout);
```

+   17. Is the following statement true or false? If it is false, correct it. In either event, explain it carefully.
+   
+   A function written using a parameter of class `ifstream` or `ofstream` can be called with `istream` or `ostream` arguments, respectively.
