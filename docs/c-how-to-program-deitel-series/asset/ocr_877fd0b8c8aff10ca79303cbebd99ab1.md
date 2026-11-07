# Section 14.4 Reading Data from a Sequential File

+   - Files store data so it may be retrieved for processing when needed.
+   - Creating an `ifstream` object opens a file for input. The `ifstream` constructor can receive the file-name and the file open mode as arguments.
+   - Open a file for input only if the file’s contents should not be modified.
+   - Objects of class `ifstream` are opened for input by default.
+   - An `ifstream` object can be created without opening a specific file; a file can be attached to it later.
+   - To retrieve data sequentially from a file, programs normally start reading from the beginning of the file and read all the data consecutively until the desired data is found.
+   - The member functions for repositioning the file-position pointer (p. 607) are `seekg` (“seek get”; p. 607) for `istream` and `seekp` (“seek put”; p. 607) for `ostream`. Each `istream` has a “get pointer,” which indicates the byte number in the file from which the next input is to occur, and each `ostream` has a “put pointer,” which indicates the byte number in the file at which the next output should be placed.
+   - The argument to `seekg` (p. 607) is a long integer. A second argument can be specified to indicate the seek direction (p. 607), which can be `ios::beg` (the default; p. 607) for positioning relative to the beginning of a stream, `ios::cur` (p. 607) for positioning relative to the current position in a stream or `ios::end` (p. 607) for positioning relative to the end of a stream.
+   - The file-position pointer (p. 607) is an integer value that specifies the location in the file as a number of bytes from the file’s starting location (i.e., the offset (p. 607) from the beginning of the file).
+   - Member functions `tellg` (p. 607) and `tellp` (p. 607) are provided to return the current locations of the “get” and “put” pointers, respectively.

# Section 14.5 Updating Sequential Files

+   - Data that is formatted and written to a sequential file cannot be modified without the risk of destroying other data in the file. The problem is that record sizes can vary in size.

# Section 14.6 Random-Access Files

+   - Sequential files are inappropriate for instant-access applications (p. 611), in which a particular record must be located immediately.
+   - Instant access is made possible with random-access files (p. 612). Individual records of a random-access file can be accessed directly (and quickly) without having to search other records.
+   - The easiest method to format files for random access is to require that all records in a file be of the same fixed length. Using same-size, fixed-length records makes it easy for a program to calculate (as a function of the record size and the record key) the exact location of any record relative to the beginning of the file.
+   - Data can be inserted into a random-access file without destroying other data in the file.
+   - Data stored previously can be updated or deleted without rewriting the entire file.

# Section 14.7 Creating a Random-Access File

+   - The `ostream` member function `write` outputs a fixed number of bytes, beginning at a specific location in memory, to the specified stream. Function `write` writes the data at the location in the file specified by the “put” file-position pointer.
+   - The `istream` member function `read` (p. 612) inputs a fixed number of bytes from the specified stream to an area in memory beginning at a specified address. If the stream is associated with a file, function `read` inputs bytes at the location in the file specified by the “get” file-position pointer.