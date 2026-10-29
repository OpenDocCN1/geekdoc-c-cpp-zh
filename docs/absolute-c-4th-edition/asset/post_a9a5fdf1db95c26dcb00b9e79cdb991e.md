
the formal parameter takes the default argument cin. If we call this as

newLine(fin);

the formal parameter takes the argument fin.
An alternative to using this newLine function is to use the function ignore, which we discussed in Chapter 9. The function ignore is a member of every input-file stream as well as a member of cin.

## Self-Test Exercises

- 13. What is the type of the stream cin? What is the type of the stream cout?

- 14. Define a function called copyChar that takes one argument that is an input stream. When called, copyChar will read one character of input from the input stream given as its argument and will write that character to the screen. You should be able to call your function using either cin or an input-file stream as the argument to your function copyChar. (If the argument is an input-file stream, then the stream is connected to a file before the function is called, so copyChar will not open or close any files.) For example, the first of the following two calls to copyChar will copy a character from the file stuff.txt to the screen, and the second will copy a character from the keyboard to the screen:

```
ifstream fin;
fin.open("stuff.txt");
copyChar(fin);
copyChar(cin);
```

- 15. Define a function called copyLine that takes one argument that is an input stream. When called, copyLine reads one line of input from the input stream given as its argument and writes that line to the screen. You should be able to call your function using either cin or an input-file stream as the argument to your function copyLine. (If the argument is an input-file stream, then the stream is connected to a file before the function is called, so copyLine will not open or close any files.) For example, the first of the following two calls to copyLine will copy a line from the file stuff.txt to the screen, and the second will copy a line from the keyboard to the screen:

```
ifstream fin;
fin.open("stuff.txt");
copyLine(fin);
copyLine(cin);
```

- 16. Define a function called sendLine that takes one argument that is an output stream. When called, sendLine reads one line of input from the keyboard and outputs the line to the output stream given as its argument. You should be able to call your function using either cout or an output-file stream as the argument to your function sendLine. (If the argument is an output-file stream, then the stream is connected to a file before the function is called, so sendLine will not open or close any files.) For example, the first of the following calls to sendLine will copy a line from the keyboard to the file morestuff.txt, and the second will copy a line from the keyboard to the screen:

```
ofstream fout;
fout.open("morestuff.txt");
cout << "Enter 2 lines of input:\n";
sendLine(fout);
sendLine(cout);
```

- 17. Is the following statement true or false? If it is false, correct it. In either event, explain it carefully.

  A function written using a parameter of class ifstream or ofstream can be called with ifstream or ofstream arguments, respectively.

## 12.4 Random Access to Files

> *Any time, any where.*

> Common response to a challenge for a confrontation

The streams for sequential access to files, which we discussed in the previous sections of this chapter, are the ones most often used for file access in C++. However, some applications that require very rapid access to records in very large databases require some sort of random access to particular parts of a file. Such applications might best be done with specialized database software. But perhaps you are given the job of writing such a package in C++, or perhaps you are just curious about how such things are done in C++. C++ does provide for random access to files so that your program can both read from and write to random locations in a file. This section gives a brief glimpse of this random access to files. This is not a complete tutorial on random access to files, but will let you know the name of the main stream class used and the important issues you will encounter.

If you want to be able to both read and write to a file in C++, you use the stream class fstream that is defined in the <fstream> library. The definition of fstream is placed in the std namespace.

Details about opening a file and connecting it to a stream in the class fstream are basically the same as discussed for the classes ifstream and ofstream, except that fstream has a second argument to open. This second argument specifies whether the stream is used for input, output, or both input and output. For example, a program that does both input and output to a file named "stuff" might start as follows:

```
#include <fstream>
using namespace std;

int main()
{
    fstream rwStream;
    rwStream.open("stuff", ios::in | ios::out);
}
```

If you prefer, you may use the following in place of the last two of the previous lines:

```
fstream rwStream("stuff", ios::in | ios::out);
```

After this, your program can read from the file "stuff" using the stream fstream and can also write to the file "stuff" using the same stream. There is no need to close and reopen the file when you change from reading to writing or from writing to reading. Moreover, you have random access for reading and writing to any location in the file. However, there are other complications.

At least two complications arise when reading and writing with random access via an fstream: (1) You normally work in bytes using the type char or arrays of char and need to handle type conversions on your own, and (2) you typically need to position a pointer (indicating where the read or write begins) before each read or write.

The constraints of finding a position and replacing one portion of a file with new data mean that most such random-access I/O is done by reading or writing records (in the form of structs or classes). One record (or an integral number of records) is read or written after each positioning of the pointer.

Each fstream object has a member function named seekp that is used to position the put-pointer at the location where you wish to write ("put") data. The function seekp takes a single argument, which is the address of the first byte to be written next. The first byte in the file is numbered zero. For example, to position the pointer in the file connected to the fstream rwStream at the 1000th byte, the invocation would be as follows:

```
rwStream.seekp(1000);
```

Of course, you need to know how many bytes a record requires. The sizeof operator can be used to determine the number of bytes needed for an object of a class or struct. Actually, sizeof can be applied to any type, object, or value. It returns the size of its argument in bytes. The operator sizeof is part of the core C++ language and requires no include directive or using directive. Some sample invocations are as follows:

- sizeof(s) (where s is string s = "Hello";)
- sizeof(10)
- sizeof(double)
- sizeof(MyStruct) (where MyStruct is a defined type)

## ANSWERS TO SELF-TEST EXERCISES

- 1. The streams `fin` and `fout` are declared as follows:

```
ifstream fin;
ofstream fout;
```

The include directive that goes at the top of your file is

```
#include <fstream>
```

Since the definitions are placed in the std namespace you should also have one of the following (or something similar):

```
using std::ifstream;
using std::ofstream;
```

or

```
using namespace std;
```

- 2.

```
fin.open("stuff1.txt");
if (fin.fail())
{
    cout << "Input file opening failed.\\n";
    exit(1);
}

fout.open("stuff2.txt");
if (fout.fail())
{
    cout << "Output file opening failed.\\n";
    exit(1);
}
```

- 3.

```
fin.close();
fout.close();
```

- 4. You need to replace the stream outStream with the stream cout. Note that you do not need to declare cout, you do not need to call open with cout, and you do not need to close cout.

- 5. This is “starting over.” The file must be closed and opened again. This action puts the read position at the start of the file, ready to be read again.

- 6.

```
1
2
3
3
```
