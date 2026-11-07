The next few sections create this credit-processing program. Figure 14.11 illustrates opening a random-access file, defining the record format using an object of class `ClientData` (Figs. 14.9–14.10) and writing data to the disk in *binary* format. This program initializes all 100 records of the file `credit.dat` with empty objects, using function `write`. Each empty object contains the account number 0, emptylast and first name strings and the balance 0.0. Each record is initialized with the space in which the account data will be stored.

```
```cpp
// Fig. 14.9: ClientData.h
// Class ClientData definition used in Fig. 14.11--Fig. 14.14.
#ifndef CLIENTDATA_H
#define CLIENTDATA_H

#include <string>

class ClientData
{
public:
   // default ClientData constructor
   ClientData( int = 0, const std::string & = "",
      const std::string & = "", double = 0.0 );

   // accessor functions for accountNumber
   void setAccountNumber( int );
   int getAccountNumber() const;

   // accessor functions for lastName
   void setLastName( const std::string & );
   std::string getLastName() const;

   // accessor functions for firstName
   void setFirstName( const std::string & );
   std::string getFirstName() const;

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
```

**Fig. 14.9**  |  *ClientData class header.*

```
```cpp
// Fig. 14.10: ClientData.cpp
// Class ClientData stores customer's credit information.
#include <string>
```
```

**Fig. 14.10**  |  *ClientData class represents a customer’s credit information. (Part 1 of 3.)*