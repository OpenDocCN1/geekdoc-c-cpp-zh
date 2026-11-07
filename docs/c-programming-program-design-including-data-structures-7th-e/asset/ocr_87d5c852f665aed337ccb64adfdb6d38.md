# # COMPLETE PROGRAM LISTING

```
~~~cpp
//***********************************************************
// Author: D.S. Malik
//
// Program: Check Code
// This program determines whether a code is transmitted
// correctly.
//***********************************************************

#include <iostream>
#include <fstream>
#include <iomanip>

using namespace std;

const int MAX_CODE_SIZE = 250;

void readCode(ifstream& infile, int list[],
              int& length, bool& lenCodeOk);
void compareCode(ifstream& infile, ofstream& outfile,
                 const int list[], int length);

int main()
{
    //Step 1
    int codeArray[MAX_CODE_SIZE]; //array to store the secret
                                  //code
    int codeLength;               //variable to store the
                                  //length of the secret code
    bool lengthCodeOk;            //variable to indicate if the length
                                  //of the secret code is less than or
                                  //equal to 250

    ifstream incode;              //input file stream variable
    ofstream outcode;             //output file stream variable

    char inputFile[51];           //variable to store the name of the
                                  //input file
    char outputFile[51];          //variable to store the name of
                                  //the output file

    cout << "Enter the input file name: ";
    cin >> inputFile;
    cout << endl;

    //Step 2
    incode.open(inputFile);
    if (!incode)
    {
        cout << "Cannot open the input file." << endl;
        return 1;
    }
}
~~~
```