# FIGURE 4.14 Demonstration Program for the String Class

# A Program

```
// FILE: str_demo.cxx (a small demonstration program showing how the string class is used)
#include <iostream> // Provides cout and cin
#include <cstdlib> // Provides EXIT_SUCCESS
#include "mystring.h" // Provides our new string class
using namespace std;

// PROTOTYPES for functions used by this demonstration program:
void match(const main_savitch_4::string& variety,
           const main_savitch_4::string& mine,
           const main_savitch_4::string& yours);
// The two strings, mine and yours, are compared. If they are the same, then a
// message is printed saying they are the same; otherwise mine is printed
// in a message. In either case, the string variety is part of the message.

int main( )
{
    const main_savitch_4::string BLANK(" ");
    const main_savitch_4::string me_first("Demo");
    main_savitch_4::string me_last("Program");
    main_savitch_4::string your_first, your_last, you;
    cout << "What is your first name? ";
    cin >> your_first;
    match("first name", me_first, your_first);
    cout << "What is your last name? ";
    cin >> your_last;
    match("last name", me_last, your_last);
    you = your_first + BLANK + your_last;
    cout << "I am happy to meet you, " << you << "." << endl;
    return EXIT_SUCCESS;
}

void match(const main_savitch_4::string& variety,
           const main_savitch_4::string& mine,
           const main_savitch_4::string& yours)
{
    if (mine == yours)
        cout << "That is the same as my " << variety << '!' << endl;
    else
        cout << "My " << variety << " is " << mine << '.' << endl;
}
```