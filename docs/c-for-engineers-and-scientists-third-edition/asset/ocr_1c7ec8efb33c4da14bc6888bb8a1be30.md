Chapter 8 443

I/O File Stream Objects and Methods

# Point of Information

Input and Output Streams

A stream is a one-way transmission path between a source and a destination. In data transmission, a stream of bytes is sent down this transmission path, similar to a stream of water providing a one-way path for water to travel from a source to a destination.
nStreams are created from stream classes. You have used two stream objects extensively the input stream named cin and the output stream object named cout. The cin object, created from the istream class, provides a transmission path from keyboard to program. The cout object, created from the ostream class, provides a transmission path from program to screen. istream and ostream classes are parent classes to the istream class. When the istream header is included in the program with the #include directive, cin and cout stream objects are declared automatically and operated by the C++ compiler.

File objects provide the same capabilities as cin and cout objects, except they connect a program to a file rather than the keyboard or screen. File stream objects must be declared explicitly as objects of the istream class (for input) or objects of the ostream class (for output). The ifstream and ofstream classes are made available by including the ifstream header with the directive #include ifstream. The ifstream class is derived from the istream and ofstream classes.

In using the open() method to connect the file's name to its internal object name, only one argument is required: the filename. For example, the following statement connects the external file named prices.dat to the internal file object named infile:

inFile.open("prices.dat");

If a file has been opened as an istream or ofstream object, the program accesses the file using the internal object name infile, and the computer saves the file under the external name prices.dat. The external filename argument passed to open() is a string encoded in double quotes. Calling the open() method requires standard object notation, in which case the name must match open(), and is preceded by an object name (infile, in this example) followed by a period.

When connecting to an existing input file stream, the file's data is available for input, starting at the first data in the file. Similarly, an output file stream creates a new file, said to be in output mode, and makes the file available for output. If a file exists with the same name as a file opened in output, the old file is erased (overwritten), and all its data is lost.
Opening a file for input or output, good practice requires checking that the connection has been established before attempting to use the file. You can do this with the fail() method, which returns a true value if the file was opened unsuccessfully (that is, it the open failed) or a false value if the operation succeeded. Typically, the fail() method is used in code similar to the following, which attempts to open a file named