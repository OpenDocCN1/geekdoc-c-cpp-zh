# CHECKING FOR THE END OF A FILE

A common way of processing an input file is to use a loop that processes data from the file until the end of the file is reached. There are two standard ways to test for the end of a file. The most straightforward way is to use the eof member function.

Every input-file stream has a member function called eof that can be used to test for reaching the end of the input file. The function eof takes no arguments, so if the input stream is called fin, then a call to the function eof is written

```
fin.eof()
```

This is a Boolean expression that can be used to control a while loop, do-while loop, or an if-else statement. This expression returns true if the program has read past the end of the input file; otherwise, it returns false.

Since we usually want to test that we are not at the end of a file, a call to the member function eof is typically used with a not in front of it. Recall that in C++ the symbol ! is used to express not. For example, the entire contents of the file connected to the input stream inStream can be written to the screen with the following while loop:

```
inStream.get(next);
while (! inStream.eof())
{
    cout << next;
    inStream.get(next);
}
```

If you prefer, you can use cout.put(next) here.

The above while loop reads each character from the input file into the char variable next using the member function get, and then it writes the character to the screen. After the program has passed the end of the file, the value of inStream.eof() changes from false to true. Thus,

(! inStream.eof())

changes from true to false and the loop ends.

Notice that inStream.eof() does not become true until the program attempts to read one character beyond the end of the file. For example, suppose the file contains the following (without any newline character after the c):

ab
c