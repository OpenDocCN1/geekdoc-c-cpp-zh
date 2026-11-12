
## G.2 Text Files

Text files are designed for easy communication with people. As such, these files are flexible and easy to use, but they are not as efficient with respect to computer time and storage as binary files.

One special aspect of text files is that they appear to be divided into lines. This illusion is often the source of much confusion. In reality, a text file—like any other file—is a sequence of bytes. That is, a text file is a sequence of characters. A special end-of-line character creates the illusion that a text file contains lines by making the file behave as if it were divided into lines.

A text file contains lines of characters

When you create a text file by typing data at your keyboard, each time you press the Enter, or Return, key, you insert one end-of-line character into the file. When an output device, such as a printer or monitor, encounters an end-of-line character in a text file, the device moves to the beginning of the next line. In C++, this end-of-line symbol is the character ‘\n’.

Files end with a special end-of-file symbol

In addition, you can think of a special end-of-file character that follows the last component in a file. Such a symbol may or may not actually exist in the file, but C++ behaves as if one did. The predefined constant EOF, for “end of file,” represents this symbol within your program. This book assumes that all text files—including the empty file—end with both an end-of-line symbol and an end-of-file symbol. Figure G-1 depicts a text file with these special symbols.

FIGURE G-1 A text file with end-of-line and end-of-file symbols

| T | o | d | a | y | [eoln] | i | s | [eoln] | [eoln] | i | t | [eoln] | [eof] |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

[eoln] is the end-of-line symbol

[eof] is the end-of-file symbol

Any program that uses files must access the standard C++ file stream library. You enable this access by including the following statements in your program:

```
#include <fstream>
using namespace std;
```

Use a stream variable to access a file

The C++ file stream library provides three stream types: ifstream for input file streams, ofstream for output file streams, and fstream for file streams that are for both input and output. You use a stream variable of one of these types to access a file. Files are sometimes referred to as streams since you can think of a file as a stream of characters flowing into or out of your program.

- 1. Open the file.
- 2. Read data from the file or write data to the file.
- 3. Close the file.

### G.2.1 Opening and Closing Text Files

You must initialize, or open, a file before you can use it

Opening a file. Before you can read from or write to a file, you need to open it. That is, you need to initialize the file and associate its name with a stream variable. One way to open a file is to provide the file’s name when you declare the stream variable. For example,

```
ifstream inFile("Ages.DAT"); // Input file
```

declares an input stream variable inFile and associates it with the file named Ages.DAT. The file name can be a literal constant, as it is here, or a string variable. Once the file is open, you no longer need the file's name; it is used only to link the file on the disk to the stream variable that you use in your program.

Alternatively, you can declare an input stream variable by writing

```
ifstream inFile;
```

and then later use the open method to associate it with the file's name:

```
inFile.open("Ages.DAT");
```

Regardless of how you open a file, you can check the stream variable to see if the process was successful by writing

```
if (!inFile) processError(); // Deal with failure to open file
```

You can check whether a file was opened successfully

**Closing a file.** You close a particular file—that is, disassociate it from a stream variable and free system resources—by using the close method:

```
myFile.close();
```

A file window marks the current position within a file

Once a file is closed, it is no longer available for input or output until a program opens it again.

### G.2.2 Reading and Writing Text Files

Associated with each file in a program is a **file window**, which marks the current position within the file. Opening a file positions the file window over the first byte in the file, as Figure G-2 illustrates. Because each byte in a text file is a character, the file window for a text file moves from character to character. The following sections describe the behavior of the file window.

Opening a text file for input positions the file window over the first character in the file

FIGURE G-2 The file window after an existing text file is opened for input

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_791_0.png)

**Character input.** Suppose that you have declared an input stream variable inFile and associated it with the name of the text file by writing

```
ifstream inFile(fileName);
```

where fileName is a string variable. When you use a file for input, the file window is over the byte that you will read next. Thus, after you open a file, you are ready to read the first byte, as you saw in Figure G-2. As you read the characters from a text file, the file window advances sequentially from one character to another. After reading several characters, you will see the file window shown in Figure G-3.

The input operator >> and methods such as get, whose use with cin was described in Appendix A, are also used with files. For the character variable ch and the stream variable inFile, either of the statements

```
inFile >> ch; // Preferred technique.
```

FIGURE G-3 A file window over the component to be read next

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_792_0.png)

or
inFile.get(ch);
means
ch = the value at the file window
Advance the file window to the next component
as Figure G-4 illustrates.

FIGURE G-4 The effect of inFile >> ch on a text file inFile

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_792_1.png)

You can detect when the file window has reached either the end of a line or the end of the file by using the peek method. This method returns the character in the file window but does not advance the window to the next character. For example, the loop

```
while (inFile.peek() != '\n') // Loop until end of line.
    cout << inFile.get(); // Get character from inFile and display it.
```

displays a line of a text file, and the loop

```
while (inFile.peek() != EOF) // Loop until end of entire file.
    cout << inFile.get(); // Get character from inFile and display it.
```

displays the contents of an entire text file.

To summarize, consider the text file inFile that appears in Figure G-4. If ch is a character variable, the statements in the following sequence assign values to ch as indicated:

```
ifstream inFile(fileName);
inFile >> ch; // ch = 'a'.
inFile.get(ch); // ch = 'b' - alternate technique 1.
ch = inFile.get(); // ch = 'c' - alternate technique 2.
inFile.ignore(10, '\n'); // Skip 'd' and end-of-file symbol.
inFile >> ch; // ch = 'e'.
ch = inFile.peek(); // ch = 'f'.
inFile >> ch; // ch = 'f'.
inFile >> ch; // ch = '\n'.
inFile.ignore(1); // Skip end-of-file symbol.
inFile >> ch; // Error: attempted read beyond end of file.
```

You also can read the characters in the file as strings by using getline, get, and read in the same way that you used them with cin.

**Character output.** Suppose that you have declared an output stream variable outFile and associated it with the name of the text file, as in

```
ofstream outFile(fileName);
```

If you are creating a new file, the file window will be positioned at the beginning (and the end) of the new file, which is empty. If the file already exists, opening it erases the data in the file and positions the window at the beginning—and the end—of the now empty file.

The output operator << and methods such as put, whose use with cout was described in Appendix A, are also used with files. For the character variable ch and the stream variable outFile, either of the statements

```
outFile << ch; // Preferred technique.
```

or

```
outFile.put(ch);
```

means

> Write the value of ch at the file-window position
> Advance the file window

Figure G-5 illustrates these steps when ch contains the character X. Note that if ch contains \n, either of the previous statements writes the end-of-line symbol to the file.

FIGURE G-5 The effect of outFile << ch on a text file outFile when ch contains the character X

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_793_0.png)

You can also write strings to a text file by using either << or the method write, as described in Appendix A.
