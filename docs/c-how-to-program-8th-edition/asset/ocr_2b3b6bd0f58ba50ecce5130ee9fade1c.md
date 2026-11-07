```
```cpp
// Screen.h
// Screen class definition. Represents the screen of the ATM.
#ifndef SCREEN_H
#define SCREEN_H

#include <string>
using namespace std;

class Screen
{
public:
    void displayMessage( string ) const; // output a message
    void displayMessageLine( string ) const; // output message with newline
    void displayDollarAmount( double ) const; // output a dollar amount
}; // end class Screen

#endif // SCREEN_H
```
```

Fig. 26.16 | Screen class definition.

```
```cpp
// Screen.cpp
// Member-function definitions for class Screen.
#include <iostream>
#include <iomanip>
#include "Screen.h" // Screen class definition
using namespace std;

// output a message without a newline
void Screen::displayMessage( string message ) const
{
    cout << message;
} // end function displayMessage

// output a message with a newline
void Screen::displayMessageLine( string message ) const
{
    cout << message << endl;
} // end function displayMessageLine

// output a dollar amount
void Screen::displayDollarAmount( double amount ) const
{
    cout << fixed << setprecision( 2 ) << "$" << amount;
} // end function displayDollarAmount
```
```

Fig. 26.17 | Screen class member-function definitions.

# Screen Class Member-Function Definitions

Figure 26.17 contains the member-function definitions for class Screen. Line 5 #includes the Screen class definition. Member function displayMessage (lines 9–12) takes a string as an argument and prints it to the console using cout and the stream insertion operator (<<). The cursor stays on the same line, making this member function appropriate for dis-