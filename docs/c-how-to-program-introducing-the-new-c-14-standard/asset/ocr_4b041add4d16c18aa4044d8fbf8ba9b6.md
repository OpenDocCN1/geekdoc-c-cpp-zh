```
```cpp
// Fig. 14.2: Fig14_02.cpp
// Creating a sequential file.
#include <iostream>
#include <string>
#include <fstream>  // contains file stream processing types
#include <cstdlib>  // exit function prototype
using namespace std;

int main() {
   // ofstream constructor opens file
   ofstream outClientFile( "clients.txt", ios::out );

   // exit program if unable to create file
   if ( !outClientFile ) {  // overloaded operator
      cerr << "File could not be opened" << endl;
      exit(EXIT_FAILURE);
   }

   cout << "Enter the account, name, and balance.\n"
        << "Enter end-of-file to end input.\n? ";

   int account;       // the account number
   string name;       // the account owner's name
   double balance;    // the account balance

   // read account, name and balance from cin, then place in file
   while ( cin >> account >> name >> balance ) {
      outClientFile << account << " " << name << " " << balance << endl;
      cout << "? ";
   }
}
```
```

```
```text
Enter the account, name, and balance.
Enter end-of-file to end input.
? 100 Jones 24.98
? 200 Doe 345.67
? 300 White 0.00
? 400 Stone -42.16
? 500 Rich 224.62
? ^Z
```
```

Fig. 14.2 Creating a sequential file.

# 14.3.1 Opening a File