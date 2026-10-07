The program has to be able to find the file.Typically, unless your input includes a path-name with the file, the program will look in the same folder or directory that contains the executable file.

> Caution
A Windows text file uses the carriage return followed by a linefeed character to terminate a line of text. (The usual C++ text translates this combination to newline character when reading a file and reverses the translation when writing to a file.) Some text editors, such as the Metroworks CodeWarrior IDE editor, don't automatically add this combination to the final line. Therefore, if you use such an editor, you need to press the Enter key typing the final edit before exiting the file.

Here's a sample run of the program in Listing 6.16:

+   Enter name of data file: `scores.txt`
End of file reached.
Items read: 12
Sum: 204.5
Average: 17.0417

# Program Notes

Instead of hard-coding a filename, the program in Listing 6.16 stores a user-supplied name in the character array filename.Then the array is used as an argument to open():`inFile.open(filename);

As discussed earlier in this chapter, it's vital to test whether the attempt to open the file succeeded. Here are a few of the things that might go wrong:The file might not exist, the file might be located in another directory or file folder, access might be denied, and the user might mistake the name or omit a extension. Many beginner has spent a long time trying to figure what's wrong with a file-reading loop when the real problem was that the program didn't open the file.Testing for opening-failure can save you such misspent effort.

You need to pay attention to the proper design of a file-reading loop.There are several things to test when reading from a file.The program should not try to read past the EOFThe `eof()` method returns true if the most recent read data into the EOF. Second, the program might encounter a type mismatch. For instance, Listing 6.16 expects a file containing only numbers.The `fail()` method returns true if the most recent read attempt encountered a type mismatch.(This method also returns true if the EOF is encountered.) Finally, something unexpected may go wrong—for a corrupted file or a hardware failure.The `bad()` method returns true if the most recent read attempt encountered a problem.Rather than test for these conditions individually, it's simpler to use the `good()` method, which returns true if nothing wrong: