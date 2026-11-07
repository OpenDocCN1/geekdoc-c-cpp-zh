```
```cpp
displayMenu();
get choice;
}//end while

PROGRAM LISTING /********************************************************************
             // Author: D.S. Malik
             //
             // This program uses the classes dvdType and dvdListType to
             // create a list of DVDs for a DVD store. It also performs
             // basic operations such as find and check out DVDs.
             //********************************************************************

#include <iostream>
#include <fstream>
#include <string>
#include "dvdType.h"
#include "dvdListType.h"

using namespace std;

void createDVDList(ifstream& infile,
                   dvdListType& dvdList);
void displayMenu();

int main()
{
        dvdListType dvdList;
        int choice;
        char ch;
        string title;

        ifstream infile;

                //open the input file
        infile.open("dvdDat.txt");
        if (!infile)
        {
                cout << "The input file does not exist. "
                     << "The program terminates!!!" << endl;
                return 1;
        }

                //create the DVD list
        createDVDList(infile, dvdList);
        infile.close();

                //show the menu
        displayMenu();
        cout << "Enter your choice: ";
        cin >> choice;       //get the request
        cin.get(ch);
        cout << endl;
```
```