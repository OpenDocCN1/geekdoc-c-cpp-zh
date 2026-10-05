# 12.4 Random Access to Files

Any time, any where.

Common response to a challenge for a confrontation

The streams for sequential access to files, which we discussed in the previous sections of this chapter, are the ones most often used for file access in C++. However, some applications that require rapid access to records in very large databases might use some sort of random access to particular parts of a file. Such applications might be best with specialized database software. But perhaps you are given the job of writing such a package in C++, or perhaps you are curious about how things are done in C++. C++ provides random access to files so that your program can both read from and write to random locations in a file. This gives a brief glimpse of this random access to files. This is not a complete tutorial on random access to files, but will let you know the name of the main stream class used and the important issues you will encounter.

If you want to be able to read and write a file in C++, use the stream class that is defined in the <fstream> library. The definition of fstream is placed in the std namespace.

Details about opening a file and connecting to a stream in the class fstream are basically the same as discussed for the classes ifstream and ofstream, except that fstream has a second argument to open. This second argument specifies whether the stream is for input, output, or both input and output. For example, a program that does both input and output to a file named "stuff" might start as:

```
#include <fstream>
using std;

int main() 
{
    fstream rwStream;
    rwStream.open("stuff", ios::in | ios::out);
```

If you prefer, use the following in place of the last two of the lines:
stream rwStream("stuff", ios::in | ios::out);

After this program, you can read from the file "stuff" using the stream fstream and also write to the file "stuff" using the same stream. There is no need to close and reopen the file when you change from reading to writing or from writing to reading. You have random access for reading and writing to any location in the file. There are other complications.

At least two complications arise when reading and writing with random access via an ifstream: (1) You normally work in bytes using the type char or arrays of char and to handle type conversions on your own, and (2) you typically need to position a pointer (indicating where the read or write begins) before each read or write.