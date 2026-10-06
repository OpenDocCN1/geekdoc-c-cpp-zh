
# APPENDIX B Understanding Numbering Systems and Computer Codes

| Decimal number | Binary number | ASCII character | Decimal number | Binary number | ASCII character |
|---|---|---|---|---|---||
| 108 | 0110 1100 | l | 118 | 0111 0110 | v |
| 109 | 0110 1101 | m | 119 | 0111 0111 | w |
| 110 | 0110 1110 | n | 120 | 0111 1000 | x |
| 111 | 0110 1111 | o | 121 | 0111 1001 | y |
| 112 | 0111 0000 | p | 122 | 0111 0010 | z Opening left brace |
| 113 | 0111 0001 | q | 123 | 0111 0011 | | Vertical line or pipe |
| 114 | 0111 0010 | r | 124 | 0111 1100 | | Closing or right brace |
| 115 | 0111 0011 | s | 125 | 0111 1101 | | |
| 116 | 0111 0100 | t | 126 | 0111 1110 | ~ Tilde |
| 117 | 0111 0101 | u | | | |

**Table B-1** Decimal and binary values for common ASCII characters

# The Hexadecimal System

The hexadecimal numbering system is a base 16 system; it uses 16 digits. As shown in Table B-2, the digits are 0 through 9 and A through F. Computer professionals often use the hexadecimal system to represent addresses and instructions as they are stored in computer memory because hexadecimal provides convenient shorthand expressions for groups of binary values. In Table B-2, each hexadecimal value represents one of the 16 possible combinations of four-digit binary values. Therefore, instead of referencing memory contents as a 16-digit binary value, for example, programmers can use a 4-digit hexadecimal value.

| Decimal value | Hexadecimal value | Binary value (shown using four digits) |
|---|---|---|
| 0 | 0 | 0000 |
| 1 | 1 | 0001 |
| 2 | 2 | 0010 |
| 3 | 3 | 0011 |
| 4 | 4 | 0100 |
| 5 | 5 | 0101 |
| 6 | 6 | 0110 |
| 7 | 7 | 0111 |
| 8 | 8 | 1000 |
| 9 | 9 | 1001 |
| 10 | A | 1010 |
| 11 | B | 1011 |
| 12 | C | 1100 |
| 13 | D | 1101 |
| 14 | E | 1110 |
| 15 | F | 1111 |

**Table B-2** Values in the decimal and hexadecimal systems

# APPENDIX B Understanding Numbering Systems and Computer Codes

In the hexadecimal system, each column is 16 times the value of the column to its right. Therefore, column values from right to left are 1, 16, 256, 4096, and so on. Figure B-3 shows how 171 and 305 are expressed in hexadecimal.

| Column value | Column value |
| --- | --- |
| 16 | 256 |
| A | B |
| 10 * 16 = 160 | 1 * 256 = 256 |
| 11 * 1 = 11 | 3 * 16 = 48 |
| -- 171 | 1 * 1 = 1 |
| | 305 |

**Figure B-3** Representing decimal values 171 and 305 in hexadecimal

# Measuring Storage

In computer systems, internal memory and external storage are measured in bits and bytes. Eight bits make a byte, and a byte frequently holds a single character (in ASCII or EBCD) or half a character (in Unicode). Because a byte is such a small unit of storage, the size of memory and files is often expressed in thousands or millions of bytes. Table B-3 describes some commonly used terms for storage.

# Understanding Numbering Systems and Computer Codes

| Term | Abbreviation | Number of bytes using binary system | Number of bytes using decimal system | Example |
|---|---|---|---|---|
| Kilobyte | KB | 1024 | one thousand | This occupies about a kilobytes. |
| Megabyte | MB | 1,048,576 (1024 kibytes) | one million | One megabyte can hold an average book in text. |
| Gigabyte | GB | 1,073,741,824 (1024 megabytes) | one billion | The hard drive on a fairly new laptop computer could be 500 gigabytes. |
| Terabyte | TB | 1024 gigabytes | one trillion | The entire library of Congress can be stored in 10 terabytes. |
| Petabyte | PB | 1024 terabytes | one quadrillion | Popular Web sites such as Google have 20 to 30 petabytes of activity per day. |
| Exabyte | EB | 1024 petabytes | one quintillion | A popular expression claims that all words spoken by humans could be stored in text form in five exabytes. |
| Zettabyte | ZB | 1024 exabytes | one sextillion | A popular expression claims that all words spoken by humans could be stored in audio form in 42 zettabytes. |
| Yottabyte | YB | 1024 zettabytes | one septillion (a 1 followed by 24 zeros) | data accessible on the Internet and in corporate networks is estimated to be yottabyte. |

**Table B-3** Commonly used terms for computer storage

In the metric system, "kilo" means 1000. However, in Table B-3, notice that a kilobyte is 1024 bytes. The discrepancy occurs because everything stored in a computer is based on the binary system; if you multiply 2 by itself 10 times, the result is 1024, which is a little more than 1000. Similarly, a gigabyte is 1,073,741,624 bytes, which is more than a billion. Confusion arises when many hard-drive manufacturers use the decimal system instead of the binary system to describe storage. For example, if you buy a hard drive that holds 10 gigabytes, it actually holds 10 billion bytes. However, in the binary system, 10 GB is 10,737,418,240 bytes, so when you check your hard drive's capacity, your computer will report that you don't quite have 10 GB, but only 9.3 GB.

# Key Terms

- The decimal numbering system is a numbering system that uses 10 digits, 0 through 9, arranged in columns to represent numbers.
- The binary numbering system is a numbering system that uses two digits, 0 and 1, arranged in columns to represent numbers.
- A bit is a binary digit.
- The American Standard Code for Information Interchange (ASCII) is an eight-bit code that represents characters.
- A byte is eight bits.
- A nibble is four bits.
- The Extended Coded Decimal Interchange Code (EBCDIC) is an eight-bit code used in IBM mainframe computers.
- Unicode is a 16-bit code used with languages such as C# and Java.
- The hexadecimal numbering system is a numbering system that uses 16 digits, 0 through 9 and A through F, arranged in columns to represent numbers.
- The base 16 system is the hexadecimal system.

# Using the IDE Editor

The Visual C# Code Editor is like a word processor for writing source code. Just as a word-processing program provides support for spelling and grammar, the C# Code Editor helps ensure your C# syntax is free from spelling and grammar errors. This support can be grouped into several categories that are described in this appendix.

# IntelliSense

IntelliSense is Microsoft's name for the set of features designed to minimize the time you spend looking for help and to help you code more accurately and efficiently. The IntelliSense features provide basic information about C# language keywords, .NET Framework types, and method signatures as you type them in the editor. The information is displayed in ToolTips, list boxes, and Smart Tags. Features of IntelliSense include:

- Providing completion lists
- Providing quick information
- Providing parameter information
- Adding using statements

# Providing Completion Lists

As you enter code in the editor, IntelliSense displays a list box that contains all of the C# keywords, .NET Framework classes, and names you have defined in your program that fit the current circumstances. This feature is called completion mode. For example, Figure C-1 shows a list box that makes suggestions based on what the programmer has typed in the Code Editor. If you find a match in the list box for the name you intend to type, you can select the item. Alternatively, you can press the Tab key to have IntelliSense finish the name or keyword for you.

# APPENDIX C Using the IDE Editor

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_734_0.png)

IntelliSense also supports a suggestion mode. In this mode, IntelliSense does not automatically complete identifiers, which makes it easier for you to type variable or method names without completion list. You can toggle between completion mode and suggestion mode by pressing Ctrl+Alt+Spacebar or by pointing to IntelliSense on the Edit menu and clicking Toggle Completion.

Similarly, when you enter a .NET Framework type or an identifier of a specific type into the Code Editor and type the dot operator (.), IntelliSense displays a list that contains the members of that type. When you don't know what method or property you want for an object, typing its identifier and a dot can direct you to the appropriate choice.

# Providing Quick Information

When you hover the cursor over a .NET Framework type, IntelliSense displays a Quick Info ToolTip that contains basic documentation about that type.

**Figure C-1** A list displayed by IntelliSense
