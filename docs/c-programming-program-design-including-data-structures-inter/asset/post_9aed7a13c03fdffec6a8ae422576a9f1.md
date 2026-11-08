
## Case 2: Sentinel-Controlled `while` Loops

You do not always know how many pieces of data (or entries) need to be read, but you may know that the last entry is a special value, called a **sentinel**. In this case, you read the first item before the while statement. If this item does not equal the sentinel, the body of the while statement executes. The while loop continues to execute as long as the program has not read the sentinel. Such a while loop is called a **sentinel-controlled while loop**. In this case, a while loop might look like the following:

```cpp
cin >> variable;             //initialize the loop control variable

while (variable != sentinel) //test the loop control variable
{
    .
    .
    .
    cin >> variable;         //update the loop control variable
    .
    .
}
```

### EXAMPLE 5-4

The program in Example 5-3 computes and outputs the total number of boxes of cookies sold, the total money made, and the average number of boxes sold by each student. However, the program assumes that the programmer knows the exact number of volunteers. Now suppose that the programmer does not know the exact number of volunteers. Once again, assume that the data is in the following format: student's name followed by a space and the number of boxes sold by the student. Because we do not know the exact number, we assume that -1 will mark the end of the data. So consider the following program:

```cpp
//Program: Sentinel-Controlled Loop
//This program computes and outputs the total number of boxes of
//cookies sold, the total revenue, and the average number of
//boxes sold by each volunteer.

#include <iostream>                                      //Line 1
#include <string>                                        //Line 2
#include <iomanip>                                       //Line 3

using namespace std;                                     //Line 4

const string SENTINEL = "-1";                           //Line 5

int main()                                               //Line 6
{
    string name;                                         //Line 8
    int numOfVolunteers;                                  //Line 9
    int numOfBoxesSold;                  //Line 10
    int totalNumOfBoxesSold;             //Line 11
    double costOfOneBox;                 //Line 12

    cout << fixed << showpoint << setprecision(2);   //Line 13

    cout << "Line 14: Enter volunteers data ending "  //Line 14
         << "with -1: " << endl;

    totalNumOfBoxesSold = 0;             //Line 15
    numOfVolunteers = 0;                 //Line 16

    cin >> name;                         //Line 17

    while (name != SENTINEL)             //Line 18
    {                                    //Line 19
        cin >> numOfBoxesSold;           //Line 20
        totalNumOfBoxesSold = totalNumOfBoxesSold
                             + numOfBoxesSold; //Line 21
        numOfVolunteers++;               //Line 22
        cin >> name;                     //Line 23
    }                                    //Line 24

    cout << endl;                        //Line 25

    cout << "Line 26: The total number of boxes sold: "
         << totalNumOfBoxesSold << endl; //Line 26

    cout << "Line 27: Enter the cost of one box: "; //Line 27
    cin >> costOfOneBox;                 //Line 28
    cout << endl;                        //Line 29

    cout << "Line 30: The total money made by selling "
         << "cookies: $"
         << totalNumOfBoxesSold * costOfOneBox << endl; //Line 30

    if (numOfVolunteers != 0)            //Line 31
        cout << "Line 32: The average number of "
             << "boxes sold by each volunteer: "
             << totalNumOfBoxesSold / numOfVolunteers
             << endl;                    //Line 32
    else
        cout << "Line 34: No input." << endl; //Line 34

    return 0;                            //Line 35
}                                        //Line 36
```

**Sample Run:** In this sample run, the user input is shaded.

```text
Line 14: Enter volunteers data ending with -1:
Sara 120
Lisa 128
Cindy 359
Nicole 267
Blair 165
Abby 290
Amy 190
Megan 450
Elizabeth 280
Meredith 290
Leslie 430
Chelsea 378
-1

Line 26: The total number of boxes sold: 3347
Line 27: Enter the cost of one box: 3.50

Line 30: The total money made by selling cookies: $11714.50
Line 32: The average number of boxes sold by each volunteer: 278
```

This program works as follows. The statements in Lines 8 to 12 declare the variables used in the program. The statement in Line 14 prompts the user to enter the data ending with -1. The statements in Lines 15 and 16 initialize the variables totalNumOfBoxesSold and numOfVolunteers. The statement in Line 17 reads the first name and stores it in name. The while statement in Line 18 checks whether name is not equal to SENTINEL. (The variable name is the loop control variable.) If name is not equal to SENTINEL, the body of the while loop executes. The statement in Line 20 reads and stores the number of boxes sold by the student in the variable numOfBoxesSold and the statement in Line 21 updates the value of totalNumOfBoxesSold by adding numOfBoxesSold to it. The statement in Line 22 increments the value of numOfVolunteers by 1, and the statement in Line 23 reads and stores the next name into name. The statements in Lines 20 through 23 repeat until the program reads the SENTINEL. The statement in Line 26 outputs the total number of boxes sold by the student in the variable totalNumOfBoxesSold, and the statement in Line 28 inputs the cost in the variable costOfOneBox. The statement in Line 30 outputs the total money made by selling cookies, and the statements in Lines 31 through 34 output the average number of boxes sold by each volunteer.

Notice that the statement in Line 17 initializes the LCV name. The expression name != SENTINEL in Line 18 checks whether the value of name is not equal to SENTINEL. The statement in Line 23 reinitializes the LCV name.

Next, consider another example of a sentinel-controlled while loop. In this example, the user is prompted to enter the value to be processed. If the user wants to stop the program, he or she can enter the sentinel.

### EXAMPLE 5-5: Telephone Digits

The following program reads the letter codes A to Z and prints the corresponding telephone digit. This program uses a sentinel-controlled while loop. To stop the program, the user is prompted for the sentinel, which is #. This is also an example of a nested control structure, in which if...else, switch, and the while loop are nested.

```cpp
//**********************************************************
// Program: Telephone Digits
// This is an example of a sentinel-controlled loop. This
// program converts uppercase letters to their corresponding
// telephone digits.
//**********************************************************

#include <iostream>

using namespace std;

int main()
{
    char letter;                                      //Line 1

    cout << "Program to convert uppercase "
         << "letters to their corresponding "
         << "telephone digits." << endl;              //Line 2

    cout << "To stop the program enter #."
         << endl;                                     //Line 3

    cout << "Enter a letter: ";                       //Line 4
    cin >> letter;                                    //Line 5
    cout << endl;                                     //Line 6

    while (letter != '#')                             //Line 7
    {
        cout << "The letter you entered is: "
             << letter << endl;                       //Line 8
        cout << "The corresponding telephone "
             << "digit is: ";                         //Line 9

        if (letter >= 'A' && letter <= 'Z')           //Line 10
            switch (letter)                           //Line 11
            {
                case 'A':
                case 'B':
                case 'C':
                    cout << 2 << endl;                //Line 12
                    break;                            //Line 13
```
