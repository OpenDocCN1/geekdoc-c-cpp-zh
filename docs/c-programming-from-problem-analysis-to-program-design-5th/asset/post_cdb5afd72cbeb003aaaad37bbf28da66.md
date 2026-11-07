
```cpp
srand(time());
num = rand() % 100;
```

The first statement sets the seed, and the second statement generates a random number greater than or equal to 0 and less than 100. Note how the function time is used. It is used with an argument, namely, 0.

The program uses the bool variable isGuessed to control the loop. The bool variable isGuessed is initialized to false. It is set to true when the user guesses the correct number.

```cpp
//Flag-controlled while loop.
//Number guessing game.

#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main()
{
        //declare the variables
        int num;             //variable to store the random
                             //number
        int guess;           //variable to store the number
                             //guessed by the user
        bool isGuessed;      //boolean variable to control
                             //the loop

        srand(time(0));                              //Line 1
        num = rand() % 100;                           //Line 2

        isGuessed = false;                            //Line 3

        while (!isGuessed)                             //Line 4
        {                                               //Line 5
                cout << "Enter an integer greater"
                     << " than or equal to 0 and"
                     << " less than 100: ";           //Line 6

                cin >> guess;                          //Line 7
                cout << endl;                          //Line 8

                if (guess == num)                      //Line 9
                {                                       //Line 10
                        cout << "You guessed the correct "
                             << "number." << endl;      //Line 11
                        isGuessed = true;               //Line 12
                }                                       //Line 13
                else if (guess < num)                  //Line 14
                        cout << "Your guess is lower than the "
                             << "number.\n Guess again!"
                             << endl;                   //Line 15
            else
                cout << "Your guess is higher than "        //Line 16
                     << "the number.\n Guess again!"
                     << endl;                               //Line 17
        } //end while                                   //Line 18

        return 0;
}
```

![](img/1fbe55537254baeb2b5b7dbaf64956ae_301_0.png)

**Sample Run:** In this sample run, the user input is shaded.

Enter an integer greater than or equal to 0 and less than 100: **45**

Your guess is higher than the number.
  Guess again!
Enter an integer greater than or equal to 0 and less than 100: **20**

Your guess is lower than the number.
  Guess again!
Enter an integer greater than or equal to 0 and less than 100: **35**

Your guess is higher than the number.
  Guess again!
Enter an integer greater than or equal to 0 and less than 100: **28**

Your guess is lower than the number.
  Guess again!
Enter an integer greater than or equal to 0 and less than 100: **32**

You guessed the correct number.

The preceding program works as follows: The statement in Line 2 creates an integer greater than or equal to 0 and less than 100 and stores this number in the variable num. The statement in Line 3 sets the bool variable isGuessed to false. The expression in the while loop at Line 4 evaluates the expression !isGuessed. If isGuessed is false, then !isGuessed is true and the body of the while loop executes; if isGuessed is true, then !isGuessed is false, so the while loop terminates.

The statement in Line 6 prompts the user to enter an integer greater than or equal to 0 and less than 100. The statement in Line 7 stores the number entered by the user in the variable guess. The expression in the if statement in Line 9 determines whether the value of guess is the same as num, that is, if the user guessed the number correctly. If the value of guess is the same as num, the statement in Line 11 outputs the message:

You guessed the correct number.

The statement in Line 12 sets the variable isGuessed to true. The control then goes back to Line 3. Because isGuessed is true, !isGuessed is false and the while loop terminates. If the expression in Line 9 evaluates to false, then the else statement in Line 14 determines whether the value of guess is less than or greater than num and outputs the appropriate message.

becomes true, so the expression:

`!infile.eof()`

in the `while` statement becomes false and the loop terminates.

> **NOTE**
>
> In the Windows console environment, the end-of-file marker is entered using Ctrl+z (hold the Ctrl key and press z). In the UNIX environment, the end-of-file marker is entered using Ctrl+d (hold the Ctrl key and press d).

### EXAMPLE 5-7

The following code uses an EOF-controlled `while` loop to find the sum of a set of numbers:

```cpp
int sum = 0;
int num;

cin >> num;

while (cin)
{
    sum = sum + num;    //Add the number to sum
    cin >> num;         //Get the next number
}

cout << "Sum = " << sum << endl;
```

### EXAMPLE 5-8

Suppose we are given a file consisting of students' names and their test scores, a number between 0 and 100 (inclusive). Each line in the file consists of a student name followed by the test score. We want a program that outputs each student's name followed by the test score followed by the grade. The program also needs to output the average test score for the class. Consider the following program:

```cpp
// This program reads data from a file consisting of students'
// names and their test scores. The program outputs each student's
// name followed by the test score followed by the grade. The
// program also outputs the average test score for all the students.

#include <iostream>                         //Line 1
#include <fstream>                          //Line 2
#include <string>                           //Line 3
#include <iomanip>                          //Line 4

using namespace std;                        //Line 5

int main()                                                              //Line 6
{                                                                        //Line 7
    //Declare variables to manipulate data
    string firstName;                                                   //Line 8
    string lastName;                                                    //Line 9
    double testScore;                                                   //Line 10
    char grade = ' ';                                                   //Line 11
    double sum = 0;                                                     //Line 12
    int count = 0;                                                      //Line 13

    //Declare stream variables
    ifstream inFile;                                                    //Line 14
    ofstream outFile;                                                   //Line 15

    //Open input file
    inFile.open("Ch5_stData.txt");                                      //Line 16

    if (!inFile)                                                        //Line 17
    {                                                                   //Line 18
        cout << "Cannot open input file. "
             << "Program terminates!" << endl;                          //Line 19
        return 1;                                                       //Line 20
    }                                                                   //Line 21
    //Open output file
    outFile.open("Ch5_stData.out");                                     //Line 22

    outFile << fixed << showpoint << setprecision(2);                   //Line 23

    inFile >> firstName >> lastName; //read the name                 //Line 24
    inFile >> testScore;             //read the test score            //Line 25

    while (inFile)                                                      //Line 26
    {                                                                   //Line 27
        sum = sum + testScore; //update sum                             //Line 28
        count++;               //increment count                        //Line 29

        //determine the grade
        switch (static_cast<int> (testScore) / 10)                      //Line 30
        {                                                               //Line 31
        case 0:                                                         //Line 32
        case 1:                                                         //Line 33
        case 2:                                                         //Line 34
        case 3:                                                         //Line 35
        case 4:                                                         //Line 36
        case 5:                                                         //Line 37
            grade = 'F';                                                //Line 38
            break;                                                      //Line 39

        case 6:                                                         //Line 40
            grade = 'D';                                                //Line 41
            break;                                                      //Line 42

        case 7:                                                         //Line 43
            grade = 'C';                                                //Line 44
            break;                                                      //Line 45
```
