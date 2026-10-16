d. If aFormula is found,

Display the location-th elements of name and specificHeat.

Else

Display a "Not Found" message.

# Example 12.3 Searching a Chemistry Database

```
/* Program to read a file containing the name, formula, and specific heat for various inorganic compounds and store these in vector<T> objects. The user then enters various formulas; the list of formulas is searched for each; if found, its name and specific heat are displayed.

Input(keyboard): name of data file and formulas (or "QUIT")
Input(file):     chemical formulas, names, and specific heats
Output(screen):  Prompts for formulas; if found, name and specific heat displayed; otherwise, a "not found" message
--------------------------------------------------------------------------*/

#include <iostream>                // cin, cout, >>, <<
#include <fstream>                 // ifstream
#include <cassert>                 // assert()
#include <string>                  // string, getline()
#include <vector>                  // vector<T>
using namespace std;

int main()
{
    cout << "Program reads chemical formulas until user enters QUIT.\n"
         "For each formula, it searches a list of formulas, and if\n"
         "the formula is found, the name and specific heat of that\n"
         "inorganic compound is displayed; otherwise,'Not Found' "
         "is displayed.\n\n";

    // Open an input stream to the file
    cout << "Enter the name of the input file: ";
    string inputFileName;
    getline(cin, inputFileName);
    ifstream inStream;
    inStream.open(inputFileName.data());
    assert( inStream.is_open() );

    // Copy contents of file into 3 vector<T>s
    string aFormula, name1, name2;
    float aSpecificHeat;
    vector<string> formula, name;
    vector<float> specificHeat;
```