# Program 9.4

```
#include <iostream>
#include <fstream>
#include <cstdlib>  // needed for exit()
#include <string>  // needed for the string class
#include <iomanip>  // needed for formatting
using namespace std;

int main()
{
    string filename = "prices.dat";  // put the filename up front
    ofstream outFile;

    outFile.open(filename.c_str());

    if (outFile.fail())
    {
        cout << "The file was not successfully opened" << endl;
        exit(1);
    }

    // set the output file stream formats
    outFile << setiosflags(ios::fixed)
            << setiosflags(ios::showpoint)
            << setprecision(2);

    // send data to the file
    outFile << "Mats " << 39.95 << endl
            << "Bulbs " << 3.22 << endl
            << "Fuses " << 1.08 << endl;

    outFile.close();
    cout << "The file " << filename
         << " has been successfully written." << endl;

    return 0;
}
```

The extra characters consist of the newline escape sequence at the end of each line created by the endl manipulator, which is created as a carriage return character (cr) and linefeed (lf). Assuming characters are stored with the ASCII code, the prices.dat file is physically stored as shown in Figure 9.2. For convenience, the character corresponding to each hexadecimal code is listed below the code. A code of 20 represents the blank character. Additionally,