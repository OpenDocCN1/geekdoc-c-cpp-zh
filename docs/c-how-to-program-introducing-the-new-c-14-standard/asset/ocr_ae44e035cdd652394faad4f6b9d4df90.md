# Section 14.2 Files and Streams

+   - C++ views each file simply as a sequence of bytes.
+   - Each file ends either with an end-of-file marker or at a specific byte number recorded in a system-maintained, administrative data structure.
+   - When a file is opened, an object is created, and a stream is associated with the object.
+   - To perform file processing in C++, headers `<iostream>` and `<fstream>` must be included.
+   - Header `<fstream>` includes the definitions for the stream class templates `basic_ifstream` (for file input), `basic_ofstream` (for file output) and `basic_fstream` (for file input and output).
+   - Each class template has a predefined template specialization that enables char I/O. The `<fstream>` library provides `typedef` aliases for these template specializations. The `typedef ifstream` represents a specialization of `basic_ifstream` that enables `char` input from a file. The `typedef ofstream` represents a specialization of `basic_ofstream` that enables `char` output to files. The `typedef fstream` represents a specialization of `basic_fstream` that enables `char` input from, and output to, files.
+   - The file-processing templates derive from class templates `basic_istream`, `basic_ostream` and `basic_iostream`, respectively.