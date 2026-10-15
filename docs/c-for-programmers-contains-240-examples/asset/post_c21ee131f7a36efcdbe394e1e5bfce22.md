
// Fig. 17.7: Fig17_07.cpp
// Reading and printing a sequential file.
#include <iostream>
using std::cerr;
using std::cout;
using std::endl;
using std::fixed;
using std::ios;
using std::left;
using std::right;
using std::showpoint;

#include <fstream> // file stream
using std::ifstream; // input file stream

#include <iomanip>
using std::setw;
using std::setprecision;

#include <string>
using std::string;

#include <cstdlib>
using std::exit; // exit function prototype

void outputLine( int, const string, double ); // prototype

int main()
{
    // ifstream constructor opens the file
    ifstream inClientFile( "clients.dat", ios::in );

    // exit program if ifstream could not open file
    if ( !inClientFile )
    {
        cerr << "File could not be opened" << endl;
        exit( 1 );
    } // end if

    int account;
    char name[ 30 ];
    double balance;

    cout << left << setw( 10 ) << "Account" << setw( 13 )
        << "Name" << "Balance" << endl << fixed << showpoint;

    // display each record in file
    while ( inClientFile >> account >> name >> balance )
        outputLine( account, name, balance );

    return 0; // ifstream destructor closes the file
} // end main

```cpp
// display single record from file
void outputLine( int account, const string name, double balance )
{
   cout << left << setw( 10 ) << account << setw( 13 ) << name
        << setw( 7 ) << setprecision( 2 ) << right << balance << endl;
} // end function outputLine
```

| Account | Name  | Balance |
|---:|---|---:|
| 100 | Jones | 24.98 |
| 200 | Doe | 345.67 |
| 300 | White | 0.00 |
| 400 | Stone | -42.16 |
| 500 | Rich | 224.62 |

Objects of class `ifstream` are opened for input by default. We could have used the statement

```cpp
ifstream inClientFile( "clients.dat" );
```

to open `clients.dat` for input. Just as with an `ofstream` object, an `ifstream` object can be created without opening a specific file, because a file can be attached to it later.

The program uses the condition `!inClientFile` to determine whether the file was opened successfully before attempting to retrieve data from the file. Line 48 reads a set of data (i.e., a record) from the file. After the preceding line is executed the first time, account has the value 100, name has the value "Jones" and balance has the value 24.98. Each time line 48 executes, it reads another record from the file into the variables account, name and balance. Line 49 displays the records, using function `outputLine` (lines 55–59), which uses parameterized stream manipulators to format the data for display. When the end of file has been reached, the implicit call to `operator void *` in the `while` condition returns the null pointer (which converts to the bool value `false`), the `ifstream` destructor function closes the file and the program terminates.

To retrieve data sequentially from a file, programs normally start reading from the beginning of the file and read all the data consecutively until the desired data is found. It might be necessary to process the file sequentially several times (from the beginning of the file) during the execution of a program. Both `istream` and `ostream` provide member functions for repositioning the *file-position pointer* (the byte number of the next byte in the file to be read or written). These member functions are `seekg` (“seek get”) for `istream` and `seekp` (“seek put”) for `ostream`. Each `istream` object has a “get pointer,” which indicates the byte number in the file from which the next input is to occur, and each `ostream` object has a “put pointer,” which indicates the byte number in the file at which the next output should be placed. The statement

```cpp
inClientFile.seekg( 0 );
```

repositions the file-position pointer to the beginning of the file (location 0) attached to `inClientFile`. The argument to `seekg` normally is a long integer. A second argument can be specified to indicate the *seek direction*, which can be `ios::beg` (the default) for positioning relative to the beginning of a stream, `ios::cur` for positioning relative to the current position.

position in a stream or ios::end for positioning relative to the end of a stream. The file-position pointer is an integer value that specifies the location in the file as a number of bytes from the file’s starting location (this is also referred to as the offset from the beginning of the file). Some examples of positioning the “get” file-position pointer are

```
// position to the nth byte of fileObject (assumes ios::beg)
fileObject.seekg( n );

// position n bytes forward in fileObject
fileObject.seekg( n, ios::cur );

// position n bytes back from end of fileObject
fileObject.seekg( n, ios::end );

// position at end of fileObject
fileObject.seekg( 0, ios::end );
```

The same operations can be performed using ostream member function seekp. Member functions tellg and tellp are provided to return the current locations of the “get” and “put” pointers, respectively. The following statement assigns the “get” file-position pointer value to variable location of type long:

```
location = fileObject.tellg();
```

Figure 17.8 enables a credit manager to display the account information for those customers with zero balances (i.e., customers who do not owe the company any money), credit (negative) balances (i.e., customers to whom the company owes money), and debit (positive) balances (i.e., customers who owe the company money for goods and services received in the past). The program displays a menu and allows the credit manager to enter one of three options to obtain credit information. Option 1 produces a list of accounts with zero balances. Option 2 produces a list of accounts with credit balances. Option 3 produces a list of accounts with debit balances. Option 4 terminates program execution. Entering an invalid option displays the prompt to enter another choice.

```
1  // Fig. 17.8: Fig17_08.cpp
2  // Credit inquiry program.
3  #include <iostream>
4  using std::cerr;
5  using std::cin;
6  using std::cout;
7  using std::endl;
8  using std::fixed;
9  using std::ios;
10 using std::left;
11 using std::right;
12 using std::showpoint;
13
14 #include <fstream>
15 using std::ifstream;
16
17  #include <iomanip>
18  using std::setw;
19  using std::setprecision;
20
21  #include <string>
22  using std::string;
23
24  #include <cstdlib>
25  using std::exit; // exit function prototype
26
27  enum RequestType { ZERO_BALANCE = 1, CREDIT_BALANCE, DEBIT_BALANCE, END };
28  int getRequest();
29  bool shouldDisplay( int, double );
30  void outputLine( int, const string, double );
31
32  int main()
33  {
34      // ifstream constructor opens the file
35      ifstream inClientFile( "clients.dat", ios::in );
36
37      // exit program if ifstream could not open file
38      if ( !inClientFile )
39      {
40          cerr << "File could not be opened" << endl;
41          exit( 1 );
42      } // end if
43
44      int request;
45      int account;
46      char name[ 30 ];
47      double balance;
48
49      // get user's request (e.g., zero, credit or debit balance)
50      request = getRequest();
51
52      // process user's request
53      while ( request != END )
54      {
55          switch ( request )
56          {
57              case ZERO_BALANCE:
58                  cout << "\nAccounts with zero balances:\n";
59                  break;
60              case CREDIT_BALANCE:
61                  cout << "\nAccounts with credit balances:\n";
62                  break;
63              case DEBIT_BALANCE:
64                  cout << "\nAccounts with debit balances:\n";
65                  break;
66          } // end switch
67
68      // read account, name and balance from file
69      inClientFile >> account >> name >> balance;
```

```
70
71     // display file contents (until eof)
72     while ( !inClientFile.eof() )
73     {
74         // display record
75         if ( shouldDisplay( request, balance ) )
76             outputLine( account, name, balance );
77
78         // read account, name and balance from file
79         inClientFile >> account >> name >> balance;
80     } // end inner while
81
82     inClientFile.clear(); // reset eof for next input
83     inClientFile.seekg( 0 ); // reposition to beginning of file
84     request = getRequest(); // get additional request from user
85     } // end outer while
86
87     cout << "End of run." << endl;
88     return 0; // ifstream destructor closes the file
89 } // end main
90
91     // obtain request from user
92 int getRequest()
93 {
94     int request; // request from user
95
96     // display request options
97     cout << "\nEnter request" << endl
98         << " 1 - List accounts with zero balances" << endl
99         << " 2 - List accounts with credit balances" << endl
100        << " 3 - List accounts with debit balances" << endl
101        << " 4 - End of run" << fixed << showpoint;
102
103     do // input user request
104     {
105         cout << "\n? ";
106         cin >> request;
107     } while ( request < ZERO_BALANCE && request > END );
108
109     return request;
110 } // end function getRequest
111
112     // determine whether to display given record
113 bool shouldDisplay( int type, double balance )
114 {
115     // determine whether to display zero balances
116     if ( type == ZERO_BALANCE && balance == 0 )
117         return true;
118
119     // determine whether to display credit balances
120     if ( type == CREDIT_BALANCE && balance < 0 )
121         return true;
```
