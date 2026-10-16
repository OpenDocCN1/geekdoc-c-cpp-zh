If progCode is 'C'
    Return "Civil".
Otherwise, if progCode is 'E'
    Return "Electrical".
Otherwise, if progCode is 'I':
    Return "Industrial".
Otherwise, if progCode is 'M'
    Return "Mechanical".
Otherwise, if progCode is 'U'
    Return "Undecided".
Otherwise
    Display an error message.
    Return the empty string.

Although we clearly could implement this algorithm using an if statement, the function in Example 8.3 solves this problem using a switch statement. Note that no break statements are required in the cases of this switch. The function uses the switch to select a return statement, and a return statement causes execution of the function to terminate.

# Example 8.3 Converting Engineering Program Codes to Names

```
/* This is a driver program to test the function engrProgram.

    Input:  a character
    Output: names of programs (Civil, Electrical, ... )
----------------------------------------------------------*/

#include <iostream>        // cin, cout, <<, >>
#include <string>          // string
using namespace std;

string engrProgram(char progCode);

int main()
{
    char code;
    cout << "Enter the code of an engineering program: ";
    cin >> code;
    cout << engrProgram(code) << endl;
}

/*----------------------------------------------------------------
    This function returns the name of an engineering program
    corresponding to a given program code.

    Receive: a character
```