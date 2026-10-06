# 10.1 Introduction to File Input and Output 381

This statement declares two things.

+   - The word OutputFile indicates the mode in which we will use the file. Our pseudocode, OutputFile indicates that we will be writing to the file.
- The name customerFile the internal name we will use to work with the output file in our code.

Although the syntax for making this declaration varies greatly among programming languages, you typically have to declare both the mode in which you will use a file and the file's internal name before you work with it.

The next step is to open the file. In our pseudocode we will use the Open statement. Here is an example:

```
Open customerFile "customers.dat"
```

The word Open is followed by an internal name that was previously declared, and a string that contains a filename. After this statement, a file name customer-dat will be created on the disk, and we will be able to use the internal name customerToFile write data to the file.

> WARNING! Remember, when you open an output file you are creating the file on the disk. In most languages, if a file with the specified external name already exists when the file is opened, the contents of the existing file will be erased.

# Writing Data to a File

Once you have opened an output file you can write data to it. In our pseudocode we will use the Write statement to write data to a file. For example:

```
Write customerFile "Charles Pace"
```

writes the "Charles Pace" to the file that is associated with customerFile. You can also write the contents of a variable to a file, as shown in the following pseudocode:

```
Declare String name = "Charles Pace"
Write customerFile name
```

The second statement in this pseudocode writes the contents of the name variable to the file associated with customerFile. (These examples show a string being written to a file, but you can also write numeric values.)

# Closing an Output File

Once a program is finished with a file, it should close the file. Closing a file disconnects the program from the file. In some systems, failure to close an output file can cause a loss of data. This happens because the data that is written to a file is first written to a buffer, which is a small "holding section" in memory. When the buffer is full, the computer operating system writes the buffer's contents to the file. This technique increases the system's performance, because writing data to memory is faster than writing to a disk. The process of closing an output file forces any unsaved data that remains in the buffer to be written to the file.