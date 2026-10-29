or "written to" a device that has been assigned as the standard output file. For most systems, it's a computer screen, although it can also be a printer.

When a program including the iostream header file is executed, the standard input stream cin is connected to the standard input device. Similarly, the standard output stream cout is connected to the standard output device. These two object streams are available for programmer use, as are the standard error stream, cerr, and the standard log stream, clog. Both these streams connect to the screen.

# Other Devices

The keyboard, display, error, and log streams are connected automatically to the stream objects cin, cout, cerr, and clog when the iostream header file is included in a program. Other devices can be used for input or output if the name the system assigns is known. For example, most PCs assign the name prn to the printer connected to the computer. For these computers, a statement such as outfile.open("prn") connects the printer to the ofstream object named outfile. A subsequent statement, such as outfile << "Hello World!";, would cause the string Hello World! to be output directly to the printer. As the name of an actual file, prn must be enclosed in double quotation marks in the open() method call.

# EXERCISES 9.2

+   1. (Practice and Modify) a. Enter and run Program 9.5.
+      b. Modify Program 9.5 to use the expression inFile.eof() in place of the expression inFile.good(), and run the program to see whether it operates correctly.

+   2. (Practice and Modify) a. Enter and run Program 9.6.
+      b. Modify Program 9.6 by replacing cout with cerr, and verify that the output for the standard error file stream is the screen.
+      c. Modify Program 9.6 by replacing cout with clog, and verify that the output for the standard log stream is the screen.

+   3. (Practice and Modify) a. Write a C++ program that accepts lines of text from the keyboard and writes each line to a file named text.dat until an empty line is entered. An empty line is a line with no text that's created by pressing the Enter (or Return) key.
+      b. Modify Program 9.6 to read and display the data stored in the text.dat file created in Exercise 3a.

+   4. (Practice) Determine the OS command or procedure your computer provides to display the contents of a saved file.

+   5. (Program) a. Create a text file named employee.dat containing the following data:

| Anthony | A | 10031 | 11.82 | 12/18/2010 |
| Burrows | W | 10067 | 12.14 | 6/9/2011 |
| Fain | B | 10083 | 10.79 | 5/18/2011 |
| Janney | P | 10095 | 12.57 | 9/28/2008 |
| Smith | G | 10105 | 9.50 | 12/20/2006 |