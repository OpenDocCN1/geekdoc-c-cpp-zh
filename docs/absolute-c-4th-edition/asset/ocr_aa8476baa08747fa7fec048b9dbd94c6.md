then calls the function newLine, which discards the rest of the input line. This means that if the user types 75 on the next input line, as shown in the sample dialogue, the program will read the number 75 and will not attempt to read the letter o in the word No. If the program did not include a call to the function newLine, then the next item read would be the o in the line containing No instead of the number 75 on the following line.

# Display 9.2 Checking Input (part 1 of 2)

```
//Program to demonstrate the functions newLine and getInput
#include <iostream>
using namespace std;

void newLine();
//Discards all the input remaining on the current input line.
//Also discards the '\n' at the end of the line.

void getInt(int& number);
//Sets the variable number to a
//value that the user approves of.

int main()
{
    int n;

    getInt(n);
    cout << "Final value read in = " << n << endl
         << "End of demonstration.\n";

    return 0;
}

//Uses iostream:
void newLine()
{
    char symbol;
    do
    {
        cin.get(symbol);
    } while (symbol != '\n');
}
//Uses iostream:
void getInt(int& number)
{
```