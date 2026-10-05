Pass anyfstream stream to the checkIOstate() function to check its state. I check the individual methods to clarify the state. At the end, I reset the state with clear() back to goodbit.

In the section starting from val=0, you will be prompted to enter a value. Correctly, you must enter an integer here. With checkIOstate, I then check the cin stream. If the input is correct, goodbit is set, and good() is true. For an incorrect input like blablubb, fail() is true.

For ifstream file, I check a file stream std::ifstream, because with I can open a file for reading. In the example, it is assumed that the file does not exist, which is why fail() is true here as well.

And finally, starting from fstream fstr, I demonstrate EOF. Between open and seek, I create a file, write something into it, and reset the data stream to the beginning. In the while loop, I read characters from the fstr stream as long as the state of fstr is equal to good() (goodbit set). either the end of the stream has been reached (eofbit is set) or an error has occurred (failbit is set). As already mentioned, fail is also set when eofbit is set.

```
Exception ios_base::failure
```

In case of errors in the I/O stream library, ios_base::failure exception can also be thrown (if badbit is set). However, this depends on the implementation of the compiler manufacturer.