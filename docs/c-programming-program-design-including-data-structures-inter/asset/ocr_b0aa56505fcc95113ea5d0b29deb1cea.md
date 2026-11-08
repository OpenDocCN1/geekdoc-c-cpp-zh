Next, consider the following statements:

```
```cpp
int numberOfLines = 15;
int numberOfBlanks = 30;

for (counter = 1; counter <= numberOfLines; counter++)
{
    printStars(numberOfBlanks, counter);
    numberOfBlanks--;
}
```
```

The for loop calls the function printStars. Every iteration of this for loop specifies the number of blanks followed by the number of stars to print in a line, using the variables numberOfBlanks and counter. Every invocation of the function printStars receives one fewer blank and one more star than the previous call. For example, the first iteration of the for loop in the main program specifies 30 blanks and 1 star (which are passed as the parameters numberOfBlanks and counter to the function printStars). The for loop then decrements the number of blanks by 1 by executing the statement, numberOfBlanks--; At the end of the for loop, the number of stars is incremented by 1 for the next iteration. This is done by executing the update statement counter++ in the for statement, which increments the value of the variable counter by 1. In other words, the second call of the function printStars receives 29 blanks and 2 stars as parameters. Thus, the previous statements will print a triangle of stars consisting of 15 lines.

```
```cpp
//Program: Print a triangle of stars

#include <iostream>

using namespace std;

void printStars(int blanks, int starsInLine);

int main()
{
    int noOfLines;    //variable to store the number of lines
    int counter;      //for loop control variable
    int noOfBlanks;   //variable to store the number of blanks

    cout << "Enter the number of star lines (1 to 20) "
         << "to be printed: ";                         //Line 1

    cin >> noOfLines;                                   //Line 2

    while (noOfLines < 0 || noOfLines > 20)             //Line 3
    {
        cout << "Number of star lines should be n"
             << "between 1 and 20" << endl;             //Line 4
        cout << "Enter the number of star lines "
             << "(1 to 20) to be printed: ";            //Line 5
        cin >> noOfLines;                                //Line 6
    }
```
```