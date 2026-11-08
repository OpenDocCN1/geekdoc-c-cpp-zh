
```cpp
else                                      //Line 16
    cout << "Your guess is higher than "
         << "the number.\nGuess again!"
         << endl;                            //Line 17
} //end while                              //Line 18

return 0;
}
```

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

The statement in Line 12 sets the variable isGuessed to true. The control then goes back to Line 4. Because isGuessed is true, !isGuessed is false, and the while loop terminates. If the expression in Line 9 evaluates to false, then the else statement in Line 14 determines whether the value of guess is less than or greater than num and outputs the appropriate message.

## Case 4: EOF-Controlled `while` Loops

If the data file is frequently altered (for example, if data is frequently added or deleted), it’s best not to read the data with a sentinel value. Someone might accidentally erase the sentinel value or add data past the sentinel, especially if the programmer and the data entry person are different people. Also, it can be difficult at times to select a good sentinel value. In such situations, you can use an **end-of-file (EOF)-controlled while loop**.

Until now, we have used an input stream variable, such as `cin`, and the extraction operator `>>`, to read and store data into variables. However, the input stream variable can also return a value after reading data, as follows:

1. If the program has reached the end of the input data, the input stream variable returns the logical value `false`.
2. If the program reads any faulty data (such as a `char` value into an `int` variable), the input stream enters the fail state. Once a stream enters the fail state, any further I/O operations using that stream are considered to be null operations; that is, they have no effect. Unfortunately, the computer does not halt the program or give any error messages. It just continues executing the program, silently ignoring each additional attempt to use that stream. In this case, the input stream variable returns the value `false`.
3. In cases other than (1) and (2), the input stream variable returns the logical value `true`.

You can use the value returned by the input stream variable to determine whether the program has reached the end of the input data. Because the input stream variable returns the logical value `true` or `false`, in a `while` loop, it can be considered a logical expression.

The following is an example of an EOF-controlled `while` loop:

```cpp
cin >> variable;    //initialize the loop control variable

while (cin)         //test the loop control variable
{
    .
    .
    .
    cin >> variable; //update the loop control variable
    .
}
```

Notice that here, the variable `cin` acts as the loop control variable.

### eof Function

In addition to checking the value of an input stream variable, such as `cin`, to determine whether the end of the file has been reached, C++ provides a function that you can use with an input stream variable to determine the end-of-file status. This function is called

becomes true, so the expression `!infile.eof()` in the while statement becomes false and the loop terminates.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_322_0.png)

In the Windows console environment, the end-of-file marker is entered using Ctrl+z (hold the Ctrl key and press z). In the UNIX environment, the end-of-file marker is entered using Ctrl+d (hold the Ctrl key and press d).

### EXAMPLE 5-7

The following code uses an EOF-controlled while loop to find the sum of a set of numbers:

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
// name followed by the test score and the grade. The program also
// outputs the average test score for all the students.

#include <iostream>                              //Line 1
#include <fstream>                               //Line 2
#include <string>                                //Line 3
#include <iomanip>                               //Line 4

using namespace std;                             //Line 5

int main()                                            //Line 6
{                                                     //Line 7
    //Declare variables to manipulate data            //Line 8
    string firstName;                                 //Line 9
    string lastName;                                  //Line 10
    double testScore;                                 //Line 11
    char grade = ' ';                                 //Line 12
    double sum = 0;                                   //Line 13
    int count = 0;                                    //Line 13

    //Declare stream variables
    ifstream inFile;                                  //Line 14
    ofstream outFile;                                 //Line 15

    //Open input file
    inFile.open("Ch5_stData.txt");                    //Line 16

    if (!inFile)                                      //Line 17
    {                                                 //Line 18
        cout << "Cannot open input file. "            //Line 19
             << "Program terminates!" << endl;        //Line 20
        return 1;                                     //Line 21
    }
    //Open output file
    outFile.open("Ch5_stData.out");                   //Line 22

    outFile << fixed << showpoint << setprecision(2); //Line 23

    inFile >> firstName >> lastName;  //read the name     Line 24
    inFile >> testScore;              //read the test score Line 25

    while (inFile)                                    //Line 26
    {                                                 //Line 27
        sum = sum + testScore; //update sum           //Line 28
        count++;              //increment count       //Line 29

        //determine the grade
        switch (static_cast<int> (testScore) / 10)    //Line 30
        {                                             //Line 31
        case 0:                                       //Line 32
        case 1:                                       //Line 33
        case 2:                                       //Line 34
        case 3:                                       //Line 35
        case 4:                                       //Line 36
        case 5:                                       //Line 37
            grade = 'F';                              //Line 38
            break;                                    //Line 39

        case 6:                                       //Line 40
            grade = 'D';                              //Line 41
            break;                                    //Line 42

        case 7:                                       //Line 43
            grade = 'C';                              //Line 44
            break;                                    //Line 45
```
