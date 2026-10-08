# File Types

In addition getting data from the keyboard and sending data to the computer screen, a program can also get data from send data to a file on a disk. Getting data from a file is referred to as “reading the file,” and sending data to a file is referred to as “writing the file.” Files to which data is written are called output files, because the files store the output produced by a program. Files that are read by the computer are input files, because a program uses the data in files as input. Input and output files are composed of lines of text that are both read and written in sequential order. In others, they are read and written one line at a time, beginning with the first line in the file and ending with the last line in the file. Such files are referred to as sequential access files, because of the manner in which the lines of text are accessed. They are also referred to as text files, because they store text. Examples of text stored in sequential access files include an employee list, and a sales report.

You can create random access and binary access files in C++. The data stored in a random access file can be accessed in consecutive or random order. The data in a binary access file can be accessed by its byte location. Random access and binary access files are less often in programs, and are not covered in this book.

# The CD Collection Program

Problem specification that keeps track of a CD (compact disc) collection. The program displays a menu containing the following options:
1 Enter CD information
2 Display CD information
3 End the program
If the user selects option 1, the program should call a function that prompts the user to enter the CD's name and the artist's name and then saves the user's entries in a sequential access file named cds.txt. If the user selects option 2, the program should call a function that displays the contents of the cds.txt file on the screen. The program should end only when the user selects option 3. If the cds.txt file cannot be opened, the program should display “File could not be opened.” message.

Figure 1-1 Problem specification and IPO charts for the CD collection program (continues)