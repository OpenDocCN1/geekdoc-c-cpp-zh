```
```cpp
// delete record, if record exists in file
if ( client.getAccountNumber() != 0 )
{
   ClientData blankClient; // create blank record

   // move file-position pointer to correct record in file
   deleteFromFile.seekp( ( accountNumber - 1 ) *
      sizeof( ClientData ) );

   // replace existing record with blank record
   deleteFromFile.write(
      reinterpret_cast< const char * >( &blankClient ),
      sizeof( ClientData ) );

   cout << "Account # " << accountNumber << " deleted.\n";
} // end if
else // display error if record does not exist
   cerr << "Account # " << accountNumber << " is empty.\n";
} // end deleteRecord

// display single record
void outputLine( ostream& output, const ClientData &record )
{
   output << left << setw( 10 ) << record.getAccountNumber()
      << setw( 16 ) << record.getLastName()
      << setw( 11 ) << record.getFirstName()
      << setw( 10 ) << setprecision( 2 ) << right << fixed
      << showpoint << record.getBalance() << endl;
} // end function outputLine

// obtain account-number value from user
int getAccount( const char * const prompt )
{
   int accountNumber;

   // obtain account-number value
   do
   {
      cout << prompt << " ( 1 - 100 ): ";
      cin >> accountNumber;
   } while ( accountNumber < 1 || accountNumber > 100 );

   return accountNumber;
} // end function getAccount
```
```

Fig. 14.14 | Bank account program. (Part 6 of 6.)

The program has five options (Option 5 is for terminating the program). Option 1 calls function createTextFile to store a formatted list of all the account information in a text file called print.txt that may be printed. Function createTextFile (lines 80–116) takes an fstream object as an argument to be used to input data from the credit.dat file. Function createTextFile invokes istream member function read (lines 102–103) and uses the sequential-file-access techniques of Fig. 14.13 to input data from credit.dat.