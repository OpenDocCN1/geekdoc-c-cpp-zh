
```cpp
// Fig. 15.6: Fig15_06.cpp
// Inputting characters using cin member function getline.
#include <iostream>
using namespace std;

int main()
{
   const int SIZE = 80;
   char buffer[ SIZE ]; // create array of 80 characters

   // input characters into buffer via cin function getline
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

Fig. 15.6 | Inputting character data with cin member function getline.

### 15.4.2 istream Member Functions peek, putback and ignore

The **ignore** member function of istream reads and discards a designated number of characters (the default is one) or terminates upon encountering a designated delimiter (the default is EOF, which causes ignore to skip to the end of the file when reading from a file).

The **putback** member function places the previous character obtained by a get from an input stream back into that stream. This function is useful for applications that scan an input stream looking for a field beginning with a specific character. When that character is input, the application returns the character to the stream, so the character can be included in the input data.

The **peek** member function returns the next character from an input stream but does not remove the character from the stream.

### 15.4.3 Type-Safe I/O

C++ offers type-safe I/O. The << and >> operators are overloaded to accept data items of specific types. If unexpected data is processed, various error bits are set, which the user may test to determine whether an I/O operation succeeded or failed. If operator << has not been overloaded for a user-defined type and you attempt to input into or output the contents of an object of that user-defined type, the compiler reports an error. This enables the program to “stay in control.” We discuss these error states in Section 15.8.

### 15.5 Unformatted I/O Using read, write and gcount

Unformatted input/output is performed using the **read** and **write** member functions of istream and ostream, respectively. Member function read inputs bytes to a character array in memory; member function write outputs bytes from a character array. These bytes are not formatted in any way. They’re input or output as raw bytes. For example, the call

```cpp
char buffer[] = "HAPPY BIRTHDAY";
cout.write( buffer, 10 );
```

outputs the first 10 bytes of buffer (including null characters, if any, that would cause output with cout and << to terminate). The call

```cpp
cout.write( "ABCDEFGHIJKLMNOPQRSTUVWXYZ", 10 );
```

displays the first 10 characters of the alphabet.

The read member function inputs a designated number of characters into a character array. If fewer than the designated number of characters are read, failbit is set. Section 15.8 shows how to determine whether failbit has been set. Member function gcount reports the number of characters read by the last input operation.

Figure 15.7 demonstrates istream member functions read and gcount, and ostream member function write. The program inputs 20 characters (from a longer input sequence) into the array buffer with read (line 13), determines the number of characters input with gcount (line 17) and outputs the characters in buffer with write (line 17).

```cpp
1   // Fig. 15.7: Fig15_07.cpp
2   // Unformatted I/O using read, gcount and write.
3   #include <iostream>
4   using namespace std;
5
6   int main()
7   {
8      const int SIZE = 80;
9      char buffer[ SIZE ]; // create array of 80 characters
10
11     // use function read to input characters into buffer
12     cout << "Enter a sentence:" << endl;
13     cin.read( buffer, 20 );
14
15     // use functions write and gcount to display buffer characters
16     cout << endl << "The sentence entered was:" << endl;
17     cout.write( buffer, cin.gcount() );
18     cout << endl;
19  } // end main
```

```text
Enter a sentence:
Using the read, write, and gcount member functions
The sentence entered was:
Using the read, writ
```

Fig. 15.7 | Unformatted I/O using the read, gcount and write member functions.

### 15.6 Introduction to Stream Manipulators

C++ provides various stream manipulators that perform formatting tasks. The stream manipulators provide capabilities such as setting field widths, setting precision, setting and

### 15.6.2 Floating-Point Precision (precision, setprecision)

We can control the precision of floating-point numbers (i.e., the number of digits to the right of the decimal point) by using either the setprecision stream manipulator or the precision member function of ios_base. A call to either of these sets the precision for all subsequent output operations until the next precision-setting call. A call to member function precision with no argument returns the current precision setting (this is what you need to use so that you can restore the original precision eventually after a “sticky” setting is no longer needed). The program of Fig. 15.9 uses both member function precision (line 22) and the setprecision manipulator (line 31) to print a table that shows the square root of 2, with precision varying from 0 to 9.

```cpp
1  // Fig. 15.9: Fig15_09.cpp
2  // Controlling precision of floating-point values.
3  #include <iostream>
4  #include <iomanip>
5  #include <cmath>
6  using namespace std;
7
8  int main()
9  {
10    double root2 = sqrt( 2.0 ); // calculate square root of 2
11    int places; // precision, vary from 0-9
12
13    cout << "Square root of 2 with precisions 0-9." << endl
14       << "Precision set by ios_base member function "
15       << "precision:" << endl;
16
17    cout << fixed; // use fixed-point notation
18
19    // display square root using ios_base function precision
20    for ( places = 0; places <= 9; places++ )
21    {
22       cout.precision( places );
23       cout << root2 << endl;
24    } // end for
25
26    cout << "\nPrecision set by stream manipulator "
27       << "setprecision:" << endl;
28
29    // set precision for each digit, then display square root
30    for ( places = 0; places <= 9; places++ )
31       cout << setprecision( places ) << root2 << endl;
32  } // end main
```

```text
Square root of 2 with precisions 0-9.
Precision set by ios_base member function precision:
1
1.4
1.41
1.414
```

Fig. 15.9 | Precision of floating-point values. (Part 1 of 2.)

```cpp
5     int main()
6     {
7         int widthValue = 4;
8         char sentence[ 10 ];
9
10
11        cout << "Enter a sentence:" << endl;
12        cin.width( 5 ); // input only 5 characters from sentence
13
14        // set field width, then display characters based on that width
15        while ( cin >> sentence )
16        {
17            cout.width( widthValue++ );
18            cout << sentence << endl;
19            cin.width( 5 ); // input 5 more characters from sentence
20        } // end while
21    } // end main
```

```text
Enter a sentence:
This is a test of the width member function
This
  is
    a
      test
        of
          the
            widt
              h
                memb
                  er
                    func
                      tion
```

Fig. 15.10 | width member function of class ios_base. (Part 2 of 2.)

[Note: When prompted for input in Fig. 15.10, the user should enter a line of text and press Enter followed by end-of-file (<Ctrl>-z on Microsoft Windows systems, <Ctrl>-d on UNIX and Macintosh systems).]

### 15.6.4 User-Defined Output Stream Manipulators

You can create your own stream manipulators.3 Figure 15.11 shows the creation and use of new nonparameterized stream manipulators bell (lines 8–11), carriageReturn (lines 14–17), tab (lines 20–23) and endLine (lines 27–30). For output stream manipulators, the return type and parameter must be of type ostream &. When line 35 inserts the endLine manipulator in the output stream, function endLine is called and line 29 outputs the escape sequence \n and the flush manipulator to the standard output stream cout. Similarly, when lines 35–44 insert the manipulators tab, bell and carriageReturn in the output stream, their corresponding functions—tab (line 20), bell (line 8) and carriageReturn (line 14) are called, which in turn output various escape sequences.
