This is actually the following list of four characters:

`abc the newline character '\n'`

The loop shown will read an 'a' and write it to the screen, then read a 'b' and write it to the screen, then read the newline character '\n' and write it to the screen, and then read a 'c' and write it to the screen. At that point the loop will have read all the characters in the file. However, `inStream.eof()` will still be false. The value of `inStream.eof()` will not change from false to true until the program tries to read one more character. That is why previous while loops end with `inStream.get(next)`. The loop needs to read one extra character in order to end the loop.

There is a special end-of-file marker at the end of a file. The member function `eof` does not change from false to true until this end-of-file marker is read. That is why the previous while loop could read one character beyond what you think of as the last character in the file. However, this end-of-file marker is not an ordinary character and should not be manipulated like an ordinary character. You can read this end-of-file marker, but you should not write it out again. If you write out the end-of-file marker, the result is unpredictable. The system automatically places this end-of-file marker at the end of each file for you.

To complicate things, the implementation of `eof` on some compilers will return true without having to read the end-of-file marker, so you may need to check your compiler’s documentation or write a short program to determine your compiler’s behavior.

# the macho way
to test for end
of file

The second way to check for the end of the file is to note (and use) the fact that a read with an extraction operator actually returns a Boolean value. The expression

```
inStream >> next
```

returns true if the read was successful and returns false when your code attempts to read beyond the end of the file. For example, the following will read all the numbers in a file of integers connected to the input stream `inStream` and compute their sum in the variable `sum`:

```
double next, sum = 0;
while (inStream >> next)
    sum = sum + next;
cout << "the sum is " << sum << endl;
```

The previous loop may look a bit peculiar, because `inStream >> next` reads a number from the stream `inStream` and returns a Boolean value. An expression involving the extraction operator `>>` is simultaneously both an action and a Boolean condition. If there is another number to be input, then the number is read and the Boolean value true is returned, so the body of the loop is executed one more time.

> Technically, the Boolean condition works this way: The returned value of the operator `>>` is an input stream reference (`istream&` or `ifstream&`), as explained in Chapter 8. This stream reference is automatically converted to a bool value. The resulting value is true if the stream was able to extract data, and false otherwise.