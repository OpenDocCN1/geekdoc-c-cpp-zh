```
//Lab14-2.cpp - saves records to a sequential access
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
void displayTotal();

int main() {
    int choice = 0;
    do {
        // get user's menu choice
        choice = getChoice();
        if (choice == 1)
            addRecords();
        else
            if (choice == 2)
                displayTotal();
        end if
    } while (choice != 3);
    return 0;
} //end of main function

//****function definitions****
int getChoice() {

    //displays menu and returns choice
    int menuChoice = 0;
    cout << "Menu Options" << endl;
    cout << "1 Add Records" << endl;
    cout << "2 Display Total Sales" << endl;
    cout << "3 Exit the program" << endl;
    cout << "Choice (1, 2, or 3)? ";
    cin >> menuChoice;
    cout << endl;
    return menuChoice;
}

void addRecords() {

//saves records to a sequential access file
```