# Chapter Summary

+   - A stream of ifstream can be connected to a file with a call to the member function open. Your program can then take input from that file.

+   - A stream of ostream can be connected to a file with a call to the member function open. Your program can then send output to that file.

+   - You should use the member function fail to check whether a call to open be successful.

+   - Stream member functions, as width, set, and precision, can be used to format output. These output functions work the same for the stream cout, which is connected to the screen, and for output streams connected to files.

+   - A function may have formal parameters of a stream type, but they must be call-by-reference parameters. They cannot be call-by-value parameters. The type ifstream can be used for an input-file stream, and the type of ostream can be used for an output-file stream. (See the next summary point for other type possibilities.)

+   - If you use ifstream (spelled without the "f") as the type for an input stream parameter, then the argument corresponding to that formal parameter can be either the stream cin or an input-file stream of ifstream. If you use ostream (spelled without the "f") as the type for an output stream parameter, then the argument corresponding to that formal parameter can be the stream cout, the stream cerr, or an output-file stream of ofstream (spelled with the "f")

+   - The member function eof can be used to test when a program has reached the end of an input file.

+   - The same input and output functions can be used to manipulate strings through the stringstream class. The stringstream class provides a simple way to create a string from variables of other data types or to read variables of other data types from a string.

# Answers to Self-Test Exercises

+   1. The streams fin and fout are declared as follows:

```
ifstream fin;
ofout fout;
```

The include directive that goes at the top of your file is

```
#include <fstream>
```

Since the definitions are placed in the std namespace you should also have one of the following (or something similar).