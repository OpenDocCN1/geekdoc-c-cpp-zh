# Getting hexed

Like binary numbers (0 and 1), hexadecimal, or “hex,” numbers are fundamental to computer programming. In base 16, the digits are 0 through 9 and then A, B, C, D, E, F — where A=10, B=11 … F=15. To illustrate (using the zero-x prefix to indicate hex):

```
0xD = 13 decimal
0x10 = 16 decimal: 1*16 + 0*1
```

```
0x2A = 42 decimal: 2*16 + A*1 (where A*1 = 10*1)
```

The alphabetic digits can be uppercase or lowercase: C is the same as c. It’s weird, but quite useful, especially when you’re debugging or working close to the metal with memory contents.

At the end of the loop, it pauses to allow the programmer a chance to gaze on the output from DumpHex().

The GetFileList() method begins by creating an empty FileInfo list. This list is the one it returns in the event of an error.

Here’s a neat trick to remember when coding any Get...List() method: If an error occurs, display an error message and return a zero-length list.

Be careful about returning a reference to an object. For instance, don’t return a reference to one of the underlying queues wrapped up in the PriorityQueue class, described in Chapter 8 of this minibook — unless you want to invite folks to mess with those queues through the reference instead of through your class methods, that is. That’s a sure ticket to a corrupt, unpredictable queue. But GetFileList() doesn’t expose the innards of one of your classes here, so it’s okay.

GetFileList() then creates a DirectoryInfo object. Just as its name implies, a DirectoryInfo object contains the same type of information about a directory that a FileInfo object does about a file: name, rank, and serial-number-type stuff. However, the DirectoryInfo object has access to one thing that a FileInfo doesn’t: a list of the files in the directory, in the form of a FileInfo array.

As usual, GetFileList() wraps the directory- and file-related code in a big try block. (For an explanation of try and catch, see Chapter 9 in this minibook.) The catch at the end traps any errors that are generated. Just to embarrass you further, the catch block flaunts the name of the directory (which probably doesn’t exist, because you entered it incorrectly).

The DumpHex() method is a little tricky only because of the difficulties in formatting the output just right.

![](bbox=[0.11, 0.48, 0.18, 0.58])

![](bbox=[0.11, 0.58, 0.18, 0.68])