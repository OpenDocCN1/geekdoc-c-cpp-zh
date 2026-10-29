With twoSumVersion1, the argument must be of type ifstream. So if fileIn is a file input stream connected to a file, then

```
twoSumVersion1(fileIn);
```

is legal, but

```
twoSumVersion1(cin); // ILLEGAL
```

is not legal, because cin is not of type ifstream. The object cin is only a stream and only of type istream; cin is not a file input stream.

The function twoSumVersion2 is more versatile. Both of the following are legal:

```
twoSumVersion2(fileIn);
twoSumVersion2(cin);
```

The moral is clear: Use istream, not ifstream, as a parameter type whenever you can. When choosing a parameter type, use the most general type you can. (To draw a real-life analogy: You might prefer to own a convertible, but you would not want a garage that could only hold a convertible. What if you borrowed a sedan from a friend? You'd still want to be able to park the sedan in your garage.)

You cannot always use the parameter type istream instead of the parameter type ifstream. If you define a function with a parameter of type istream, then that parameter can only use istream member functions. In particular, it cannot use the functions open and close. If you cannot keep all calls to the member functions open and close outside the function definition, then you must use a parameter of type ifstream.

So far we have discussed two classes for input streams: istream and its derived class ifstream. The situation with output streams is similar: Chapter 1 introduced the output streams cout and cerr, which are in the class ostream. This chapter introduced the file output streams, which are in the class ofstream (with an 'f'). The class ostream is the class of all output streams. The streams cout and cerr are of type ostream, but not of type ofstream. In contrast to cout or cerr, an output-file stream is declared to be of type ofstream. The class ofstream of output-file streams is a derived class of the class ostream. For example, the following function writes the word "Hello" to the output stream given as its argument.

```
void sayHello(ostream& anyOutStream)
{
    anyOutStream << "Hello";
}
```

The first of the following calls writes "Hello" to the screen; the second writes "Hello" to the file with the external file name afile.txt.

```
ofstream fout;
fout.open("afile.txt");
sayHello(cout);
sayHello(fout);
```