# 468 I/O Streams and Data Files

Program 8.7 initially goes to the last character in the file. The offset of the EOF character, is saved in the variable last. Because tellg() returns a long integer, last has been declared as a long integer.

Starting from the end of the file, seek() is used to position the next character to be read, referenced from the end of the file. As each character is read, the character is displayed, and the offset is adjusted to access the next character. The first offset used is -1, which represents the character immediately preceding the EOF marker.

![](bbox=[0.105, 0.263, 0.168, 0.313])

# EXERCISES 8.3

+   1. (Practice) Create a file named test.dat containing the data in the test.dat file used in Program 8.7. (You can use a text editor or copy the test.dat file from your book's Web site).
b. Enter and execute Program 8.7 on your computer.
2. (Modify) Rewrite Program 8.7 so that the origin for the seekg() method used in the loop is the start of the file rather than the end.
3. (Modify) Program 8.7 to display an error message if seekg() attempts to refer a position beyond the end of the file.
4. (Practice) Write a program that reads and displays every second character in a file named test.dat.
5. (Practice) Using the seek() and tell() methods, write a function named fileChars() that returns the total number of characters in a file.
6. (Practice) Write a function named readBytes that reads and displays n characters starting from any position in the file. The function should accept three arguments: a file object, the name of the first character to be read, and the number of characters to be read. (Note: The prototype for readBytes() is void readBytes(fstream&, int)).
b. Modify the readBytes() function written in Exercise 6a to store the characters read into a string or an array. The function should accept as a fourth argument.

# 8.4 File Streams as Function Arguments

A stream object can be used as a function argument. The only requirement is that the function's formal parameter be a reference (see Section 6.3) to the appropriate stream, istream or ofstream. For example, in Program 8.8, an ofstream object named outFile is opened in main(), and this stream object is passed to the inOut() function. The function prototype and header for inOut() declare the formal parameter as a reference to an ofstream object type. The inOut() function is then used to write five lines of user-entered text to the file.