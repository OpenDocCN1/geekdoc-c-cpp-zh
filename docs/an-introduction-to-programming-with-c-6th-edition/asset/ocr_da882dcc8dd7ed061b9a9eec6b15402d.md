# CHAPTER 14

# Sequential Access Files

# LAB 14-5 Debug

Follow the instructions for starting C++ and opening the Lab14-5.cpp file. The file is contained in the Cpp6\Chapter14\Lab14-5 Project folder or the Cpp6\Chapter14 folder. Debug the program.

# Summary

+   - Sequential access files can be either input files or output files. Input files are files whose contents are read by a program. Output files are files to which a program writes data.

+   - To create a object in a program, the program must contain the #include <fstream> directive.

+   - You use the ifstream and ofstream classes, which are defined in the fstream file, to create input and output file objects, respectively. The file objects are used to represent the actual files stored on your computer's disk.

+   - After creating a file object, you use the open function to open the file for input, or output.

+   - You can use the is_open function to determine whether the open function succeeded or failed to open a access file. The is_open function returns the Boolean value true if the open function was able to open the file. It returns the Boolean false if the open function could not open the file.

+   - To distinguish one record from another in a sequential access file, programmers usually write each record on a separate line at the end of the statement that writes the record to the file. You do this by including the endl manipulator at the end. If the record contains more than one field, use a character (such as '#') to separate the data in one field from another.

+   - When reading data from a file, you use the eof function to determine whether the pointer is at the end of the file. If the file pointer is located after the last character in the file, the eof function returns the Boolean value true; otherwise, it returns the Boolean value false.

+   - When a program is finished with a file, you should use the close function to close it. Failing to close an open file can result in the loss of data.

# Terms

- !The logical operator

close function—closes a sequential access file in a program

eof function—determines whether an entire access file has been read; it returns true when the file pointer is located after the last character in a sequential access file; otherwise, it returns false