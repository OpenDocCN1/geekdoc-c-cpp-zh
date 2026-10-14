things whether you intend to read or write this file. (The mode variable is also a string.) To open the file input.dat for reading you might call

```
ifp = fopen("input.dat", "r");
```

The mode string "r" indicates reading. Mode "w" indicates writing, so we could open output.dat for output like this:

```
ofp = fopen("output.dat", "w");
```

The other values for the mode string are less frequently used. The third major mode is "a" for append. (If you use "w" to write to a file which already exists, its old contents will be discarded.) You may also add "+" character to the mode string to indicate that you want to both read and write, or a "b" character to indicate that you want to do "binary" (as opposed to text) I/O.

One thing to beware of when opening files is that it's an operation which may fail. The requested file might not exist, or it might be protected against reading or writing. (These possibilities ought to be obvious, but it's easy to forget them.) fopen returns a null pointer if it can't open the requested file, and it's important to check for this case before going off and using fopen's return value as a file pointer. Every call to fopen will typically be followed with a test, like this:

```
ifp = fopen("input.dat", "r");
if(ifp == NULL)
{
printf("can't open file\n");
exit or return
}
```

If fopen returns a null pointer, and you store it in your file pointer variable and go off and try to do I/O with it, your program will typically crash. It's common to collapse the call to fopen and the assignment in with the test: