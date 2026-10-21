+   3. What is the advantage of files ?
+   4. How text file different from binary file ?
+   5. Discuss function for random access of a file.
+   6. What are the opening modes ? Explain the purpose of each mode.
+   7. What are command line arguments ? How do we use them in our program ?
+   8. How can we read write object from/to file ?
+   9. What are various error handling functions C++ provides ?
+   10. What is eof ? How it can detect end of file ?

# C. Brain Drill :

+   1. Write a program that displays on the screen the contents of text file line by line backwards. It should be possible to run your program by providing the file name as a command line argument.
+   2. Write a C++ class to read an existing file and create another file with all words of the source file stored in reverse order. It is assumed that successive words are separated by one or more white space characters.
+   3. Write a C++ program to compare contents of two files whose names are supplied through the command line. Display the first line having mismatch along with its number.
+   4. Write a C++ program to copy the alternate lines in reverse order from a source file to target file with the file names are entered at the command prompt.
+   5. Write a program that emulates the DOS COPY command. That is, it should copy the contents of a text file (such as any .CPP file) to another file. Invoke the program with two command-line arguments—the source file and the destination file-like this :
+   C>copy srcfile.cpp destfile.cpp
+   In the program, check that the user has typed the correct number of command-line arguments, and that the files specified can be opened.
+   6. Write a program that returns the size in bytes of a program entered on the command line :
+   C>filesize program.exe
+   7. In a loop, prompt the user to enter name data consisting of a first name, middle initial, last name, and employee number (type unsigned long). Then, using formatted I/O with the insertion (<<) operator, write these four data items to an ofstream object. Don't forget that strings must be terminated with a space or other white space character. When the user indicates that no more name data will be entered, close the ofstream object, open an ifstream object, read and display all the data in the file, and terminate the program.
+   8. Create a time class that includes integer member values for hours, minutes, and seconds. Make a member function get_time ( ) that gets a time value from the user, and a function put_time ( ) that displays a time in 12 :59 :59 format. Add error checking to the get_time ( ) function to minimize user mistake. This function should request hours, minutes, and second separately, and check each one for ios error status flags and the correct range. Hours should be between 0 and 23, and minutes and seconds between 0 to 59. Don't input these values as strings and then convert them; read them directly as integers. This implies that you won't be able to screen out entries with superfluous decimal points.
+   In main ( ), use a loop to repeatedly get a time vale from the user with get_time ( ) and then display it with put_time ( ), like this :
+   Enter hours : 11
+   Enter minutes : 59
+   Enter seconds : 59
+   Time = 11 :59 :59
+   Do another (y/n) ? y