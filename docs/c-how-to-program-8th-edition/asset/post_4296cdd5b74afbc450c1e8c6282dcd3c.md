
stream or `ios::end` for positioning relative to the end of a stream. The file-position pointer is an integer value that specifies the location in the file as a number of bytes from the file’s starting location (this is also referred to as the `offset` from the beginning of the file). Some examples of positioning the get file-position pointer are

```cpp
// position to the nth byte of fileObject (assumes ios::beg)
fileObject.seekg(n);

// position n bytes forward in fileObject
fileObject.seekg(n, ios::cur);

// position n bytes back from end of fileObject
fileObject.seekg(n, ios::end);

// position at end of fileObject
fileObject.seekg(0, ios::end);
```

The same operations can be performed using ostream member function `seekp`. Member functions `tellg` and `tellp` are provided to return the current locations of the get and put pointers, respectively. The following statement assigns the get file-position pointer value to variable location of type long:

```cpp
location = fileObject.tellg();
```

Figure 17.7 enables a credit manager to display the account information for those customers with zero balances (i.e., customers who do not owe the company any money), credit (negative) balances (i.e., customers to whom the company owes money), and debit (positive) balances (i.e., customers who owe the company money for goods and services received in the past). The program displays a menu and allows the credit manager to enter one of three options to obtain credit information. Option 1 produces a list of accounts with zero balances. Option 2 produces a list of accounts with credit balances. Option 3 produces a list of accounts with debit balances. Option 4 terminates program execution. Entering an invalid option displays the prompt to enter another choice. Lines 65–66 enable the program to read from the beginning of the file after the EOF marker has been read.

```cpp
// Fig. 17.7: Fig17_07.cpp
// Credit inquiry program.
#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>
#include <cstdlib>
using namespace std;

enum RequestType { ZERO_BALANCE = 1, CREDIT_BALANCE, DEBIT_BALANCE, END };
int getRequest();
bool shouldDisplay(int, double);
void outputLine(int, const string, double);

int main()
{
    // ifstream constructor opens the file
    ifstream inClientFile("clients.txt", ios::in);

    // exit program if ifstream could not open file
    if ( !inClientFile )
    {
        cerr << "File could not be opened" << endl;
        exit( 1 );
    } // end if

    int request;
    int account;
    string name;
    double balance;

    // get user's request (e.g., zero, credit or debit balance)
    request = getRequest();

    // process user's request
    while ( request != END )
    {
        switch ( request )
        {
            case ZERO_BALANCE:
                cout << "\nAccounts with zero balances:\n";
                break;
            case CREDIT_BALANCE:
                cout << "\nAccounts with credit balances:\n";
                break;
            case DEBIT_BALANCE:
                cout << "\nAccounts with debit balances:\n";
                break;
        } // end switch

        // read account, name and balance from file
        inClientFile >> account >> name >> balance;

        // display file contents (until eof)
        while ( !inClientFile.eof() )
        {
            // display record
            if ( shouldDisplay( request, balance ) )
                outputLine( account, name, balance );

            // read account, name and balance from file
            inClientFile >> account >> name >> balance;
        } // end inner while

        inClientFile.clear(); // reset eof for next input
        inClientFile.seekg( 0 ); // reposition to beginning of file
        request = getRequest(); // get additional request from user
    } // end outer while

    cout << "End of run." << endl;
} // end main

// obtain request from user
int getRequest()
{
    int request; // request from user

    // display request options
    cout << "\nEnter request" << endl
         << " 1 - List accounts with zero balances" << endl
         << " 2 - List accounts with credit balances" << endl
         << " 3 - List accounts with debit balances" << endl
         << " 4 - End of run" << fixed << showpoint;

    do // input user request
    {
        cout << "\n? ";
        cin >> request;
    } while ( request < ZERO_BALANCE || request > END );

    return request;
} // end function getRequest

// determine whether to display given record
bool shouldDisplay( int type, double balance )
{
    // determine whether to display zero balances
    if ( type == ZERO_BALANCE && balance == 0 )
        return true;

    // determine whether to display credit balances
    if ( type == CREDIT_BALANCE && balance < 0 )
        return true;

    // determine whether to display debit balances
    if ( type == DEBIT_BALANCE && balance > 0 )
        return true;

    return false;
} // end function shouldDisplay

// display single record from file
void outputLine( int account, const string name, double balance )
{
    cout << left << setw( 10 ) << account << setw( 13 ) << name
         << setw( 7 ) << setprecision( 2 ) << right << balance << endl;
} // end function outputLine
```

```text
Enter request
  1 - List accounts with zero balances
  2 - List accounts with credit balances
  3 - List accounts with debit balances
  4 - End of run
? 1
```

**Fig. 17.7** | Credit inquiry program.

today’s popular 32-bit machines). However, these integers become different-sized fields when output as formatted text (character sequences). Therefore, the formatted input/output model usually is not used to update records in place.

Such updating can be done awkwardly. For example, to make the preceding name change, the records before 300 White 0.00 in a sequential file could be copied to a new file, the updated record then rewritten to the new file, and the records after 300 White 0.00 copied to the new file. This requires processing every record in the file to update one record. If many records are being updated in one pass of the file, though, this technique can be acceptable.

## 17.6 Random-Access Files

So far, we’ve seen how to create sequential files and search them to locate information. Sequential files are inappropriate for instant-access applications, in which a particular record must be located immediately. Common instant-access applications are airline reservation systems, banking systems, point-of-sale systems, automated teller machines and other kinds of transaction-processing systems that require rapid access to specific data. A bank might have hundreds of thousands (or even millions) of other customers, yet, when a customer uses an automated teller machine, the program checks that customer’s account in a few seconds or less for sufficient funds. This kind of instant access is made possible with random-access files. Individual records of a random-access file can be accessed directly (and quickly) without having to search other records.

As we’ve said, C++ does not impose structure on a file. So the application that wants to use random-access files must create them. A variety of techniques can be used. Perhaps the easiest method is to require that all records in a file be of the same fixed length. Using same-size, fixed-length records makes it easy for a program to calculate (as a function of the record size and the record key) the exact location of any record relative to the beginning of the file. We’ll soon see how this facilitates immediate access to specific records, even in large files.

Figure 17.8 illustrates C++’s view of a random-access file composed of fixed-length records (each record, in this case, is 100 bytes long). A random-access file is like a railroad train with many same-size cars—some empty and some with contents.

![](img/bfd978e7e9b192bab46ec2a89e481263_703_0.png)

**Fig. 17.8** | *C++ view of a random-access file.*

Data can be inserted into a random-access file without destroying other data in the file. Data stored previously also can be updated or deleted without rewriting the entire file. In the
