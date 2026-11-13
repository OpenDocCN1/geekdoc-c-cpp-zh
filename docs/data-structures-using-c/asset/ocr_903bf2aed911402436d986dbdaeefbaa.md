# PROGRAM CODE 14.4

```
```cpp
//Index sequential file (one to one map index)
#include <stdio.h>
#include <conio.h>
#include<iostream.h>
#include<fstream.h>
/* Item record */
struct itemrec
{
    int itemcode;
    char itemname[20];
    float cost;
};
/* Index record */
struct indexrec
{
    int itemcode;
    int position;
    int flag;
};
/* Display the contents of index file */
void displayindexfile()
{
    fstream indexfile;
    struct indexrec index;
    indexfile.open("index.dat", ios::in);
    cout << "\n Index file is n";
    cout << "\n Itemcode \t Position \t Del Flag";
    while(!indexfile.eof())
    {
        indexfile.read((char*)&index, sizeof(indexrec));
        if(indexfile.eof())
            break;
        if(index.flag == 1)
            cout << endl << index.itemcode <<
            index.position<<index.flag;
        else
            cout << *deleted*;
            cout << endl << index.itemcode <<
            index.position << index.flag;
    }
}
```
```