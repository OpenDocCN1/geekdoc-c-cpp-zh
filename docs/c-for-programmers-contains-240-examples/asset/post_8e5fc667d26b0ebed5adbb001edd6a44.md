
Each stream object contains a set of *state bits* used to control the state of the stream (i.e., formatting, setting error states, etc.). These bits are used by the stream’s overloaded void * cast operator to determine whether to return a non-null pointer or the null pointer. Stream extraction causes the stream’s *failbit* to be set if data of the wrong type is input and causes the stream’s *badbit* to be set if the operation fails. Section 15.7 and Section 15.8 discuss stream state bits in detail, then show how to test these bits after an I/O operation.

## 15.4.1 get and getline Member Functions

The *get* member function with no arguments inputs one character from the designated stream (including white-space characters and other nongraphic characters, such as the key sequence that represents end-of-file) and returns it as the value of the function call. This version of get returns EOF when end-of-file is encountered on the stream.

## Using Member Functions eof, get and put

Figure 15.4 demonstrates the use of member functions eof and get on input stream cin and member function put on output stream cout. The program first prints the value of cin.eof()—i.e., false (0 on the output)—to show that end-of-file has not occurred on cin. The user enters a line of text and presses Enter followed by end-of-file (<Ctrl>-z on Microsoft Windows systems, <Ctrl>-d on UNIX and Macintosh systems). Line 17 reads each character, which line 18 outputs to cout using member function put. When end-of-file is encountered, the while statement ends, and line 22 displays the value of cin.eof(), which is now true (1 on the output), to show that end-of-file has been set on cin. Note that this program uses the version of istream member function get that takes no arguments and returns the character being input (line 17). Function eof returns true only after the program attempts to read past the last character in the stream.

```
1  // Fig. 15.4: Fig15_04.cpp
2  // Using member functions get, put and eof.
3  #include <iostream>
4  using std::cin;
5  using std::cout;
6  using std::endl;
7
8  int main()
9  {
10     int character; // use int, because char cannot represent EOF
11
12     // prompt user to enter line of text
13     cout << "Before input, cin.eof() is " << cin.eof() << endl
14        << "Enter a sentence followed by end-of-file:" << endl;
15
16     // use get to read each character; use put to display it
17     while ( ( character = cin.get() ) != EOF )
18         cout.put( character );
19
20     // display end-of-file character
21     cout << "\nEOF in this system is: " << character << endl;
22     cout << "After input of EOF, cin.eof() is " << cin.eof() << endl;
23     return 0;
24 } // end main
```

Fig. 15.4 | get, put and eof member functions. (Part 1 of 2.)

```
Before input, cin.eof() is 0
Enter a sentence followed by end-of-file:
Testing the get and put member functions
Testing the get and put member functions
^Z

EOF in this system is: -1
After input of EOF, cin.eof() is 1
```

Fig. 15.4 | get, put and eof member functions. (Part 2 of 2.)

The get member function with a character-reference argument inputs the next character from the input stream (even if this is a white-space character) and stores it in the character argument. This version of get returns a reference to the istream object for which the get member function is being invoked.

A third version of get takes three arguments—a character array, a size limit and a delimiter (with default value '\n'). This version reads characters from the input stream. It either reads one fewer than the specified maximum number of characters and terminates or terminates as soon as the delimiter is read. A null character is inserted to terminate the input string in the character array used as a buffer by the program. The delimiter is not placed in the character array but does remain in the input stream (the delimiter will be the next character read). Thus, the result of a second consecutive get is an empty line, unless the delimiter character is removed from the input stream (possibly with cin.ignore()).

## Comparing cin and cin.get

Figure 15.5 compares input using stream extraction with cin (which reads characters until a white-space character is encountered) and input using cin.get. Note that the call to cin.get (line 24) does not specify a delimiter, so the default '\n' character is used.

```
1  // Fig. 15.5: Fig15_05.cpp
2  // Contrasting input of a string via cin and cin.get.
3  #include <iostream>
4  using std::cin;
5  using std::cout;
6  using std::endl;
7
8  int main()
9  {
10   // create two char arrays, each with 80 elements
11   const int SIZE = 80;
12   char buffer1[ SIZE ];
13   char buffer2[ SIZE ];
14
15  // use cin to input characters into buffer1
16  cout << "Enter a sentence:" << endl;
17  cin >> buffer1;
18
19  // display buffer1 contents
20  cout << "\nThe string read with cin was:" << endl
21      << buffer1 << endl << endl;
22
23  // use cin.get to input characters into buffer2
24  cin.get( buffer2, SIZE );
25
26  // display buffer2 contents
27  cout << "The string read with cin.get was:" << endl
28      << buffer2 << endl;
29      return 0;
30  } // end main
```

Fig. 15.5 | Input of a string using cin with stream extraction contrasted with input using cin.get. (Part 1 of 2.)

Enter a sentence:
**Contrasting string input with cin and cin.get**

The string read with cin was:
Contrasting

The string read with cin.get was:
string input with cin and cin.get

Fig. 15.5 | Input of a string using cin with stream extraction contrasted with input using cin.get. (Part 2 of 2.)

## Using Member Function getline

Member function getline operates similarly to the third version of the get member function and inserts a null character after the line in the character array. The getline function removes the delimiter from the stream (i.e., reads the character and discards it), but does not store it in the character array. The program of Fig. 15.6 demonstrates the use of the getline member function to input a line of text (line 15).

```
1  // Fig. 15.6: Fig15_06.cpp
2  // Inputting characters using cin member function getline.
3  #include <iostream>
4  using std::cin;
5  using std::cout;
6  using std::endl;
7
8  int main()
9  {
10     const int SIZE = 80;
11     char buffer[ SIZE ]; // create array of 80 characters
12
```

Fig. 15.6 | Inputting character data with cin member function getline. (Part 1 of 2.)

output stream and skipping white space in the input stream. These features are described in the following sections.

## 15.6.1 Integral Stream Base: dec, oct, hex and setbase

Integers are interpreted normally as decimal (base-10) values. To change the base in which integers are interpreted on a stream, insert the hex manipulator to set the base to hexadecimal (base 16) or insert the oct manipulator to set the base to octal (base 8). Insert the dec manipulator to reset the stream base to decimal. These are all sticky manipulators.

The base of a stream also may be changed by the setbase stream manipulator, which takes one integer argument of 10, 8, or 16 to set the base to decimal, octal or hexadecimal, respectively. Because setbase takes an argument, it is called a parameterized stream manipulator. Using setbase (or any other parameterized manipulator) requires the inclusion of the <iomanip> header file. The stream base value remains the same until changed explicitly; setbase settings are “sticky.” Figure 15.8 demonstrates stream manipulators hex, oct, dec and setbase.

```
// Fig. 15.8: Fig15_08.cpp
// Using stream manipulators hex, oct, dec and setbase.
#include <iostream>
using std::cin;
using std::cout;
using std::dec;
using std::endl;
using std::hex;
using std::oct;

#include <iomanip>
using std::setbase;

int main()
{
    int number;

    cout << "Enter a decimal number: ";
    cin >> number; // input number

    // use hex stream manipulator to show hexadecimal number
    cout << number << " in hexadecimal is: " << hex
         << number << endl;

    // use oct stream manipulator to show octal number
    cout << dec << number << " in octal is: "
         << oct << number << endl;

    // use setbase stream manipulator to show decimal number
    cout << setbase( 10 ) << number << " in decimal is: "
         << number << endl;
    return 0;
} // end main
```

Fig. 15.8 | Stream manipulators hex, oct, dec and setbase. (Part 1 of 2.)
