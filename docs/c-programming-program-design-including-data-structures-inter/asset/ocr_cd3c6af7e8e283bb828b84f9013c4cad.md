```
```cpp
{
    if (!stack.isEmptyStack())
    {
        result = stack.top();
        stack.pop();

        if (stack.isEmptyStack())
            outF << result << endl;
        else
            outF << " (Error: Too many operands)" << endl;
    } //end if
    else
        outF << " (Error in the expression)" << endl;
}
else
    outF << " (Error in the expression)" << endl;

outF << "______________________________"
     << endl << endl;
} //end printResult
```
```

# PROGRAM LISTING

```
```cpp
////////////////////////////////////////////////////////////
// Author: D.S. Malik
//
// Program: Postfix Calculator
// This program evaluates postfix expressions.
////////////////////////////////////////////////////////////

#include <iostream>
#include <iomanip>
#include <fstream>
#include "mystack.h"

using namespace std;

void evaluateExpression(ifstream& inF, ofstream& outF,
                        stackType<double>& stack,
                        char& ch, bool& isExpOk);

void evaluateOpr(ofstream& outF, stackType<double>& stack,
                 char& ch, bool& isExpOk);

void discardExp(ifstream& in, ofstream out, char& ch);
void printResult(ofstream& outF, stackType<double>& stack,
                 bool isExpOk);

int main()
{
    bool expressionOk;
    char ch;
```
```