9. No answer required.

10. No answer required.

11. Change the outFile.open("movies.txt", ios::out); state- in Line 18 to outFile.open("movies.txt", ios::app);

# LAB 14-2 Plan and Create

No answer required.

# LAB 14-3 Modify

```
//Lab14-3.cpp - saves records to a sequential access
//file and also calculates and displays the total
//of the sales amounts stored in the file
//Created/revised by <your name> on <current date>
#include <iostream>
#include <string>
#include <fstream>
using namespace std;

//function prototypes
int getChoice();
void addRecords();
void displayRecords();
void displayTotal();
void displayAvg();

int main()
{
  int choice = 0;
  do
    //get user's menu choice
      choice = getChoice();
      if (choice == 1)
        addRecords();
      else
        if (choice == 2)
          displayRecords();
        else
          if (choice == 3)
            displayTotal();
          else
            if (choice == 4)
              displayAvg();
    //end if
```