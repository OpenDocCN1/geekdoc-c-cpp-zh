
Next, consider the following statements:

```cpp
int numberOfLines = 15;
int numberOfBlanks = 30;

for (counter = 1; counter <= numberOfLines; counter++)
{
    printStars(numberOfBlanks, counter);
    numberOfBlanks--;
}
```

The for loop calls the function printStars. Every iteration of this for loop specifies the number of blanks followed by the number of stars to print in a line, using the variables numberOfBlanks and counter. Every invocation of the function printStars receives one fewer blank and one more star than the previous call. For example, the first iteration of the for loop in the main program specifies 30 blanks and 1 star (which are passed as the parameters numberOfBlanks and counter to the function printStars). The for loop then decrements the number of blanks by 1 by executing the statement, numberOfBlanks--; At the end of the for loop, the number of stars is incremented by 1 for the next iteration. This is done by executing the update statement counter++ in the for statement, which increments the value of the variable counter by 1. In other words, the second call of the function printStars receives 29 blanks and 2 stars as parameters. Thus, the previous statements will print a triangle of stars consisting of 15 lines.

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
        cout << "Number of star lines should be "
             << "between 1 and 20" << endl;             //Line 4
        cout << "Enter the number of star lines "
             << "(1 to 20) to be printed: ";            //Line 5
        cin >> noOfLines;                                //Line 6
    }

    cout << endl << endl;                         //Line 7
    noOfBlanks = 30;                              //Line 8

    for (counter = 1; counter <= noOfLines; counter++) //Line 9
    {
        printStars(noOfBlanks, counter);          //Line 10
        noOfBlanks--;                              //Line 11
    }

    return 0;                                     //Line 12
}

void printStars(int blanks, int starsInLine)
{
    int count;

    for (count = 1; count <= blanks; count++)  //Line 13
        cout << ' ';                           //Line 14
    for (count = 1; count <= starsInLine; count++) //Line 15
        cout << "*";                           //Line 16
    cout << endl;
}
```

**Sample Run:** In this sample run, the user input is shaded.

Enter the number of star lines (1 to 20) to be printed: **15**

```
              *
             * *
            * * *
           * * * *
          * * * * *
         * * * * * *
        * * * * * * *
       * * * * * * * *
      * * * * * * * * *
     * * * * * * * * * *
    * * * * * * * * * * *
   * * * * * * * * * * * *
  * * * * * * * * * * * * *
 * * * * * * * * * * * * * *
* * * * * * * * * * * * * * *
```

In the function main, the user is first asked to specify how many lines of stars to print (Line 1). (In this program, the user is restricted to 20 lines because a triangular grid of up to 20 lines fits nicely on the screen.) Because the program is restricted to only 20 lines, the while loop at Lines 3 through 6 ensures that the program prints only the triangular grid of stars if the number of lines is between 1 and 20.

## Value Parameters

The previous section defined two types of parameters—value parameters and reference parameters. Example 6–10 showed a program that uses a function with parameters. Before considering more examples of void functions with parameters, let us make the following observation about value and reference parameters. When a function is called, the value of the actual parameter is copied into the corresponding formal parameter. If the formal parameter is a value parameter, then after copying the value of the actual parameter, there is no connection between the formal parameter and actual parameter; that is, the formal parameter has its own copy of the data. Therefore, during program execution, the formal parameter manipulates the data stored in its own memory space. The program in Example 6–11 further illustrates how a value parameter works.

### EXAMPLE 6-11

The following program shows how a formal parameter of a simple data type works.

```cpp
//Example 6-11
//Program illustrating how a value parameter works.

#include <iostream>

using namespace std;

void funcValueParam(int num);

int main()
{
    int number = 6;                                      //Line 1

    cout << "Line 2: Before calling the function "
         << "funcValueParam, number = " << number
         << endl;                                        //Line 2

    funcValueParam(number);                              //Line 3

    cout << "Line 4: After calling the function "
         << "funcValueParam, number = " << number
         << endl;                                        //Line 4

    return 0;
}

void funcValueParam(int num)
{
    cout << "Line 5: In the function funcValueParam, "
         << "before changing, num = " << num
         << endl;                                        //Line 5

    num = 15;                                             //Line 6
```

Reference parameters are useful in three situations:

- When the value of the actual parameter needs to be changed
- When you want to return more than one value from a function (recall that the return statement can return only one value)
- When passing the address would save memory space and time relative to copying a large amount of data

The first two situations are illustrated throughout this book. Chapters 8 and 10 discuss the third situation, when arrays and classes are introduced.

Recall that when you attach & after the dataType in the formal parameter list of a function, the variable following that dataType becomes a reference parameter.

> You can declare a reference (formal) parameter as a constant by using the keyword `const`. Chapters 9 and 10 discuss constant reference parameters. Until then, the reference parameters that you will be using will be nonconstant as defined in this chapter. From the definition of a reference parameter, it follows that a constant value or an expression cannot be passed to a nonconstant reference parameter. If a formal parameter is a nonconstant reference parameter, during a function call, its corresponding actual parameter must be a variable.

### EXAMPLE 6-12: Calculate Grade

The following program takes a course score (a value between 0 and 100) and determines a student’s course grade. This program has three functions: `main`, `getScore`, and `printGrade`, as follows:

1. `main`
   - Get the course score.
   - Print the course grade.
2. `getScore`
   - Prompt the user for the input.
   - Get the input.
   - Print the course score.
3. `printGrade`
   - Calculate the course grade.
   - Print the course grade.

The complete program is as follows:

```cpp
//This program reads a course score and prints the
//associated course grade.

#include <iostream>
using namespace std;

void getScore(int& score);
void printGrade(int score);

int main()
{
    int courseScore;

    cout << "Line 1: Based on the course score, \n"
         << "    this program computes the "
         << "course grade." << endl;        //Line 1

    getScore(courseScore);                   //Line 2

    printGrade(courseScore);                 //Line 3

    return 0;
}

void getScore(int& score)
{
    cout << "Line 4: Enter course score: ";  //Line 4
    cin >> score;                            //Line 5
    cout << "Line 6: Course score is "
         << score << endl;                   //Line 6
}

void printGrade(int cScore)
{
    cout << "Line 7: Your grade for the course is "; //Line 7

    if (cScore >= 90)
        cout << "A." << endl;               //Line 8
    else if (cScore >= 80)
        cout << "B." << endl;
    else if (cScore >= 70)
        cout << "C." << endl;
    else if (cScore >= 60)
        cout << "D." << endl;
    else
        cout << "F." << endl;
}
```
