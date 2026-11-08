# 27.3.2 Methods for Unformatted Input

When reading raw data with methods, unlike formatted reading with >>, leading whitespace characters are not simply skipped and ignored. For unformatted input, the header file <istream> offers several methods, some of which are overloaded multiple times.

The following is an overview of the methods for unformatted input in <istream>:

+   - `istream& get(char& c);`
+     Extracts a single character from the stream into c.
+   - `istream& get(char* s, streamsize n);`
+     This reads n-1 characters from the stream and stores them as a C string in s. If fewer than n-1 characters are used, reading continues until the first newline character '\n'. The newline character is not stored in s. The null terminator '\0' is automatically added at the end.
+   - `istream& get(char* s, streamsize n, char delim);`
+     This reads n-1 characters from the stream and stores them as a C string in s. If fewer than n-1 characters are used, it reads up to the first delimiter character contained in delim. The delim character is not stored in s. The termination character '\0' is automatically appended at the end.
+   - `istream& getline(char* s, streamsize n[, char delim]);`
+     The main difference from the corresponding get() versions is that the failbit error flag is set if more than n-1 characters are read.
+   - `istream& read(char* s, streamsize n);`
+     This extracts n (not n-1) characters from the stream and stores them in C string s. Unlike the get and getline versions, the read sequence is not terminated with the null character '\0' — a classic function for copying entire blocks of data.

For all versions where you extract n–1 characters from the stream into the address of char* s, you must ensure that there is enough memory space available in s. All methods return the stream istream. Whether the input was successful can/should be checked using the mechanisms available in the <ios> header file (Section 27.4). Extracting characters from a stream is terminated in all input methods when EOF is read.

> > **End of File**
> >
> > EOF is often defined with the value –1 and is used to indicate the end of a data stream or file. In an interactive shell, you can also generate EOF with a key combination. In classic Unix shells, you can reproduce this with [Ctrl]+[D]. In the Windows command prompt, EOF is generated using [Ctrl]+[Z].

The following simple listing demonstrates some of the methods for unformatted input.