# EOF Ends Input

Remember when a cin method detects the EOF, it sets a flag in the cin object, indicating the EOF condition. When this flag is set, cin does not read any more input, and further calls to cin have no effect. For file input, this makes sense because you. For keyboard input, however, you might use a simulated EOF to terminate a loop but then read more input later. The cin.clear() method clears the EOF flag and lets input proceed again. Chapter 17, "Input, Output, and Files," discusses this further. Keep in mind, however, that in some systems, Ctrl+Z effectively terminates input and output beyond the powers of cin.clear() to restore them.

# Common Idioms for Character Input

The following is the essential design of a loop to read text character at a time until EOF:

```
cin.get(ch); // attempt to read a char
while (cin.fail() == false) // test for EOF
{
    // do stuff
    cin.get(ch); // attempt to read another char
}
```

There are some shortcuts you can take with this code. Chapter 6 introduces the operator, which toggles true to false and vice versa. You can rewrite the while loop to look like this:

```
while (!cin.fail()) // while input has not failed
```

The return value for the cin.get(char) method is cin, an object. However, the istream class provides a function that can convert an istream object such as cin to a bool value; this conversion function is called when cin occurs in a loop where bool is expected, such as in the test condition of a while loop. Furthermore, the bool value for the conversion is true if the last attempted read was successful and false otherwise. This means you can rewrite the while loop like this:

```
while (cin) // while input is successful
```

This is a bit more general than using cin.fail() or !cin.eof() because it detects other possible causes of failure, such as disk failure.

Finally, because the return value of cin.get(char) is cin, you can condense the loop to this format:

```
while (cin.get(ch)) // while input is successful
{
    // do stuff
}
```

Here, cin.get(char) is called once in the test condition indent—once before the loop and at the end of the loop. To evaluate the loop test, the program