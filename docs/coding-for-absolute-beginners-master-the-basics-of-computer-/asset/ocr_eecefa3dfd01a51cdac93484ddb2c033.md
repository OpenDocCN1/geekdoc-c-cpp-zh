In python programming, regular expressions are used to extract information from text including documents, log files, spreadsheets, or code. Regular expressions are known as characters in special order that allow programmers to find relevant sequence or characters or set of strings by using a specialized syntax. Whenever regular expressions are written in Python programming language, we are supposed to begin raw strings with prefix ‘r’ and other special meta characters as well.

# Match Function

The match() function is used to check whether the given regular expression matches a string in Python or not. In case the pattern does not match, we can use the re.match() function.

# Search Function

This function attempts to search for all of the possible starting points within the string and scans through the input string to match any location. It includes the search() or re.search() functions.

# Split Function

The split function can be applied directly on a string whereas the re.split() accepts a pattern which specifies the delimiter.

# File I/O

File is a specific location on a disk which is used to store information and data. As it is stored in a hard disk, we can also perform read and write operations by implementing python programming methods and techniques. File operation in Python consists of three major aspects which are open a file, read or write it, and close the file.

Open() is the built-in function in Python programming language which has two parameters known as filename and mode. The following methods can be implemented to perform different operations in a file:

+   - “r” = Open or read a file.
+   - “w” = Write into a file and create a new file if it does not exist.
+   - “a” = Open the file for appending and create a new file if it does not exist.
+   - “x” = Create a new file and return an error if file is already present.
+   - “t” = Open in text mode.
+   - “b” = Open in binary mode.
+   - “+” = Open file for reading or writing purpose.