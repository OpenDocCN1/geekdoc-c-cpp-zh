```
// Fig. 17.10: ClientData.h
// Class ClientData definition used in Fig. 17.12-Fig. 17.15.
#ifndef CLIENTDATA_H
#define CLIENTDATA_H

#include <string>
using std::string;

class ClientData
{
public:
    // default ClientData constructor
    ClientData( int = 0, string = "", string = "", double = 0.0 );

    // accessor functions for accountNumber
    void setAccountNumber( int );
    int getAccountNumber() const;

    // accessor functions for lastName
    void setLastName( string );
    string getLastName() const;

    // accessor functions for firstName
    void setFirstName( string );
    string getFirstName() const;

    // accessor functions for balance
    void setBalance( double );
    double getBalance() const;
private:
    int accountNumber;
    char lastName[ 15 ];
    char firstName[ 10 ];
    double balance;
}; // end class ClientData

#endif
```

Fig. 17.10 | ClientData class header file.

Objects of class string do not have uniform size, rather they use dynamically allocated memory to accommodate strings of various lengths. This program must maintain fixed-length records, so class ClientData stores the client’s first and last name in fixed-length char arrays. Member functions setLastName (Fig. 17.11, lines 37–45) and setFirstName (Fig. 17.11, lines 54–62) each copy the characters of a string object into the corresponding char array. Consider function setLastName. Line 40 initializes the const char * lastNameValue with the result of a call to string member function data, which returns an array containing the characters of the string. [Note: This array is not guaranteed to be null terminated.] Line 41 invokes string member function size to get the length of lastNameString. Line 42 ensures that length is fewer than 15 characters, then line 43 copies length characters from lastNameValue into the char array lastName. Member function setFirstName performs the same steps for the first name.