# Answers to TRY THIS Exercises

# Pencil and Paper

+   1. ifstream inSales;

+   2. outjan.open("jansales.txt");orJan.open("jansales txt", ios::out);

# Computer

+   16. See Figures 14-25 and 14-26.

```
//TryThis16.cpp - writes 26 letters to a sequential
//access file
//Created/revised by <name> on <current date>

#include <iostream>
#include <fstream>
using namespace std;

int main() 
{
    char letter = ' ';

    //create file object and open the file
    ofstream outfile;
    outfile.open("TryThis16.txt");

    //determine whether the file was opened
    if (outfile.is_open())
        //get the 26 letters of the alphabet and
        //write each to the file
        for (int x = 1; x <= 26; x = x + 1) {
            cout << "Enter letter " << x << ":";
            cin >> letter;
            outfile << letter << endl;
        }
        //close the file
        outfile.close();
    else {
        cout << "The file could not be opened." << endl;
    }
    return 0;
} //end of main function
```

> In Line 22, you can also use either x += 1 or x++.

Figure 14-25