
returns the character being input (line 15). Function `eof` returns true only after the program attempts to read past the last character in the stream.

The get member function with a character-reference argument inputs the next character from the input stream (even if this is a white-space character) and stores it in the character argument. This version of get returns a reference to the istream object for which the get member function is being invoked.

A third version of get takes three arguments—a character array, a size limit and a delimiter (with default value '\n'). This version reads characters from the input stream. It either reads one fewer than the specified maximum number of characters and terminates or terminates as soon as the delimiter is read. A null character is inserted to terminate the input string in the character array used as a buffer by the program. The delimiter is not placed in the character array but does remain in the input stream (the delimiter will be the next character read). Thus, the result of a second consecutive get is an empty line, unless the delimiter character is removed from the input stream (possibly with `cin.ignore()`).

```cpp
// Fig. 15.4: Fig15_04.cpp
// Using member functions get, put and eof.
#include <iostream>
using namespace std;

int main()
{
   int character; // use int, because char cannot represent EOF

   // prompt user to enter line of text
   cout << "Before input, cin.eof() is " << cin.eof() << endl;
        << "Enter a sentence followed by end-of-file: " << endl;

   // use get to read each character; use put to display it
   while ( ( character = cin.get() ) != EOF )
      cout.put( character );

   // display end-of-file character
   cout << "\nEOF in this system is: " << character << endl;
   cout << "After input of EOF, cin.eof() is " << cin.eof() << endl;
} // end main
```

```text
Before input, cin.eof() is 0
Enter a sentence followed by end-of-file:
Testing the get and put member functions
Testing the get and put member functions
^Z

EOF in this system is: -1
After input of EOF, cin.eof() is 1
```

**Fig. 15.4** | get, put and eof member functions.

## Comparing `cin` and `cin.get`

Figure 15.5 compares input using stream extraction with `cin` (which reads characters until a white-space character is encountered) and input using `cin.get`. The call to `cin.get` (line 22) does not specify a delimiter, so the default '\n' character is used.

```cpp
// Fig. 15.5: Fig15_05.cpp
// Contrasting input of a string via cin and cin.get.
#include <iostream>
using namespace std;

int main()
{
   // create two char arrays, each with 80 elements
   const int SIZE = 80;
   char buffer1[ SIZE ];
   char buffer2[ SIZE ];

   // use cin to input characters into buffer1
   cout << "Enter a sentence: " << endl;
   cin >> buffer1;

   // display buffer1 contents
   cout << "\nThe string read with cin was:" << endl
        << buffer1 << endl << endl;

   // use cin.get to input characters into buffer2
   cin.get( buffer2, SIZE );

   // display buffer2 contents
   cout << "\nThe string read with cin.get was:" << endl
        << buffer2 << endl;

} // end main
```

```text
Enter a sentence:
Contrasting string input with cin and cin.get

The string read with cin was:
Contrasting

The string read with cin.get was:
 string input with cin and cin.get
```

Fig. 15.5 | Contrasting input of a string via cin and cin.get.

## Using Member Function `getline`

Member function `getline` operates similarly to the third version of the `get` member function and inserts a null character after the line in the character array. The `getline` function removes the delimiter from the stream (i.e., reads the character and discards it), but does not store it in the character array. The program of Fig. 15.6 demonstrates the use of the `getline` member function to input a line of text (line 13).

```cpp
// Fig. 15.6: Fig15_06.cpp
// Inputting characters using cin member function getline.
#include <iostream>
using namespace std;

int main()
{
   const int SIZE = 80;
   char buffer[SIZE]; // create array of 80 characters

   // input characters in buffer via cin function getline
   cout << "Enter a sentence: " << endl;
   cin.getline( buffer, SIZE );

   // display buffer contents
   cout << "\nThe sentence entered is:" << endl << buffer << endl;
} // end main
```

```text
Enter a sentence:
Using the getline member function

The sentence entered is:
Using the getline member function
```

Fig. 15.6 | Inputting characters with cin member function `getline`. (Part 1 of 2.)

**Fig. 15.6** | Inputting characters with cin member function getline. (Part 2 of 2.)

## 15.4.2 istream Member Functions peek, putback and ignore

The **ignore** member function of istream reads and discards a designated number of characters (the default is one) or terminates upon encountering a designated delimiter (the default is EOF, which causes ignore to skip to the end of the file when reading from a file).

The **putback** member function places the previous character obtained by a get from an input stream back into that stream. This function is useful for applications that scan an input stream looking for a field beginning with a specific character. When that character is input, the application returns the character to the stream, so the character can be included in the input data.

The **peek** member function returns the next character from an input stream but does not remove the character from the stream.

## 15.4.3 Type-Safe I/O

C++ offers type-safe I/O. The << and >> operators are overloaded to accept data items of specific types. If unexpected data is processed, various error bits are set, which the user may test to determine when an I/O operation succeeded or failed. If operators << and >> have not been overloaded for a user-defined type and you attempt to input into or output the contents of an object of that user-defined type, the compiler reports an error. This enables the program to "stay in control." We discuss these error states in Section 15.8.

## 15.5 Unformatted I/O Using read, write and gcount

Unformatted input/output is performed using the **read** and **write** member functions of istream and ostream, respectively. Member function read inputs bytes to a character array in memory; member function write outputs bytes from a character array. These bytes are not formatted in any way. They're input or output as raw bytes. For example, the call

```cpp
char buffer[] = "HAPPY BIRTHDAY";
cout.write( buffer, 10 );
```

outputs the first 10 bytes of buffer (including null characters, if any, that would cause output with cout and << to terminate). The call

```cpp
cout.write("ABCDEFGHIJKLMNOPQRSTUVWXYZ", 10);
```

displays the first 10 characters of the alphabet.

The read member function inputs a designated number of characters into a character array. If fewer than the designated number of characters are read, failbit is set. Section 15.8 shows how to determine whether failbit has been set. Member function **gcount** reports the number of characters read by the last input operation.

Figure 15.7 demonstrates istream member functions read and gcount, and ostream member function write. The program inputs 20 characters (from a longer input sequence) into the array buffer with read (line 13), determines the number of characters input with gcount (line 17) and outputs the characters in buffer with write (line 17).

```cpp
// Fig. 15.7: Fig15_07.cpp
// Unformatted I/O using read, gcount and write.
#include <iostream>
using namespace std;

int main()
{
   const int SIZE = 80;
   char buffer[SIZE]; // create array of 80 characters

   // use function read to input characters into buffer
   cout << "Enter a sentence: " << endl;
   cin.read( buffer, 20 );

   // use functions write and gcount to display buffer characters
   cout << endl << "The sentence entered was: " << endl;
   cout.write( buffer, cin.gcount() );
   cout << endl;
} // end main
```

```text
Enter a sentence:
Using the read, write, and gcount member functions
The sentence entered was:
Using the read, writ
```

**Fig. 15.7**  Unformatted I/O using the read, gcount and write member functions.

## 15.6 Introduction to Stream Manipulators

C++ provides various **stream manipulators** that perform formatting tasks. The stream manipulators provide capabilities such as setting field widths, setting precision, setting and unsetting format state, setting the fill character in fields, flushing streams, inserting a newline into the output stream (and flushing the stream), inserting a null character into the output stream and skipping white space in the input stream. These features are described in the following sections.
