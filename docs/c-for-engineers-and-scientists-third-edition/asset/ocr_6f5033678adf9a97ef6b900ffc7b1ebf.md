# 444 I/O Streams and Data Files

prices.dat for input, checks that a valid connection was made, and reports an error
message if the file wasn't opened successfully:

```
ifstream inFile; // any object name can be used here
inFile.open("prices.dat"); // open the file
// check that the connection was successfully opened
if (inFile.fail())
{
    cout << "\nthe file was not successfully opened\n"
         << "\nPlease check that the file currently exists.\\n"
         << endl;
}
```

If the fail() method returns a true, indicating the open failed, this code displays an
er message. The exit() function is a request to the OS to end
program execution immediately, it is called. The cstlib header function must be included
in any program using exit(), and exit() single-integer argument is passed directly to
t OS for any further program action or user insertion. Throughout the remainder of
book, this type of error checking is included when a file is opened.(Section 9.2 shows
how to use exception handling for the same type of error checking.) In addition to the
fail() method, C++ provides three other methods, listed in Table 8.2, for protecting a file's
status.

# Table 8.2 File Status Methods

| Prototype | Description |
| fail() | Returns a Boolean true if the file hasn't been opened
successfully; otherwise, returns a Boolean false value. |
| eof() | Returns a Boolean true if a read has been attempted past
t end-of-file; otherwise, returns a Boolean false value.
The value becomes true only when the first character
after the last valid character is read. |
| good() | Returns a Boolean true value while the file is available
program use. Returns a Boolean false value if a read has
been attempted past the end-of-file. The value becomes
false only when the first character after the last valid file
character is read. |
| bad() | Returns a Boolean true if a read has been
attempted past the end-of-file; otherwise, returns a false.
The value becomes true only when the first character
after the last valid character is read. |

Program 8.1 shows the statements to open a file for input, including an
error-checking routine to ensure that the open was successful. A file opened for input is
to be in read mode or input mode.(These two terms are synonyms.)