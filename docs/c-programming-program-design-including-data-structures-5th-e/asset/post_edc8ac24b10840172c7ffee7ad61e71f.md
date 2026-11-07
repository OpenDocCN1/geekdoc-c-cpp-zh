
```cpp
double percentDonation;
double grossAmount;
double amountDonated;
double netSaleAmount;
```

Because movieName is declared as a string variable, you need to include the header file string. Therefore, the program needs, among others, the following include statement:

```cpp
#include <string>
```

### Formatting Output

In the output, the first column is left-justified and the numbers in the second column are right-justified. Therefore, when printing a value in the first column, the manipulator left is used; before printing a value in the second column, the manipulator right is used. The empty space between the first and second columns is filled with dots; the program uses the manipulator setfill to accomplish this goal. In the lines showing the gross amount, amount donated, and net sale amount, the space between the $ sign and the number is filled with blank spaces. Therefore, before printing the dollar sign, the program uses the manipulator setfill to set the filling character to blank. The following statements accomplish the desired output:

```cpp
cout << "-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*"
     << "-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*" << endl;
cout << setfill('.') << left << setw(35) << "Movie Name: "
     << right << " " << movieName << endl;
cout << left << setw(35) << "Number of Tickets Sold: "
     << setfill(' ') << right << setw(10)
     << noOfAdultTicketsSold + noOfChildTicketsSold
     << endl;
cout << setfill('.') << left << setw(35) << "Gross Amount: "
     << setfill(' ') << right << "$ "
     << setw(8) << grossAmount << endl;
cout << setfill('.') << left << setw(35)
     << "Percentage of Gross Amount Donated: "
     << setfill(' ') << right
     << setw(9) << percentDonation << '%' << endl;
cout << setfill('.') << left << setw(35) << "Amount Donated: "
     << setfill(' ') << right << "$ "
     << setw(8) << amountDonated << endl;
cout << setfill('.') << left << setw(35) << "Net Sale: "
     << setfill(' ') << right << "$ "
     << setw(8) << netSaleAmount << endl;
```

### MAIN ALGORITHM

In the preceding sections, we analyzed the problem and determined the formulas to do the calculations. We also determined the necessary variables and named constants. We can now expand the previous algorithm to solve the problem given at the beginning of this programming example.

- 1. Declare the variables.
- 2. Set the output of the floating-point numbers to two decimal places in a fixed decimal format with a decimal point and trailing zeros. Include header file `iomanip`.
- 3. Prompt the user to enter a movie name.
- 4. Input (read) the movie name. Because the name of a movie might contain more than one word (and, therefore, might contain blanks), the program uses the function `getline` to input the movie name.
- 5. Prompt the user to enter the price of an adult ticket.
- 6. Input (read) the price of an adult ticket.
- 7. Prompt the user to enter the price of a child ticket.
- 8. Input (read) the price of a child ticket.
- 9. Prompt the user to enter the number of adult tickets sold.
- 10. Input (read) the number of adult tickets sold.
- 11. Prompt the user to enter the number of child tickets sold.
- 12. Input (read) the number of child tickets sold.
- 13. Prompt the user to enter the percentage of the gross amount donated.
- 14. Input (read) the percentage of the gross amount donated.
- 15. Calculate the gross amount.
- 16. Calculate the amount donated.
- 17. Calculate the net sale amount.
- 18. Output the results.

### COMPLETE PROGRAM LISTING

```cpp
//************************************************************
// Author: D.S. Malik
//
// Program: Movie Tickets Sale
// This program determines the money to be donated to a
// charity. It prompts the user to input the movie name, adult
// ticket price, child ticket price, number of adult tickets
// sold, number of child tickets sold, and percentage of the
// gross amount to be donated to the charity.
//************************************************************

#include <iostream>
#include <iomanip>
#include <string>

using namespace std;

int main()
{
    //Step 1
    string movieName;
    double adultTicketPrice;
    double childTicketPrice;
    int noOfAdultTicketsSold;
    int noOfChildTicketsSold;
    double percentDonation;
    double grossAmount;
    double amountDonated;
    double netSaleAmount;

    cout << fixed << showpoint << setprecision(2);  //Step 2

    cout << "Enter the movie name: ";                 //Step 3
    getline(cin, movieName);                          //Step 4
    cout << endl;

    cout << "Enter the price of an adult ticket: ";  //Step 5
    cin >> adultTicketPrice;                          //Step 6
    cout << endl;

    cout << "Enter the price of a child ticket: ";   //Step 7
    cin >> childTicketPrice;                          //Step 8
    cout << endl;

    cout << "Enter the number of adult tickets "
         << "sold: ";                                 //Step 9
    cin >> noOfAdultTicketsSold;                      //Step 10
    cout << endl;

    cout << "Enter the number of child tickets "
         << "sold: ";                                 //Step 11
    cin >> noOfChildTicketsSold;                      //Step 12
    cout << endl;

    cout << "Enter the percentage of donation: ";     //Step 13
    cin >> percentDonation;                           //Step 14
    cout << endl << endl;

    //Step 15
    grossAmount = adultTicketPrice * noOfAdultTicketsSold +
                  childTicketPrice * noOfChildTicketsSold;

    //Step 16
    amountDonated = grossAmount * percentDonation / 100;

    netSaleAmount = grossAmount - amountDonated;       //Step 17

    //Step 18: Output results
    cout << "**********************"
         << "**********************" << endl;

    cout << setfill('.') << left << setw(35) << "Movie Name: "
         << right << " " << movieName << endl;
    cout << left << setw(35) << "Number of Tickets Sold: "
         << setfill(' ') << right << setw(10)
         << noOfAdultTicketsSold + noOfChildTicketsSold
         << endl;
    cout << setfill('.') << left << setw(35)
         << "Gross Amount: "
         << setfill(' ') << right << " $"
         << setw(8) << grossAmount << endl;
    cout << setfill('.') << left << setw(35)
         << "Percentage of Gross Amount Donated: "
         << setfill(' ') << right
         << setw(9) << percentDonation << '%' << endl;
    cout << setfill('.') << left << setw(35)
         << "Amount Donated: "
         << setfill(' ') << right << " $"
         << setw(8) << amountDonated << endl;
    cout << setfill('.') << left << setw(35) << "Net Sale: "
         << setfill(' ') << right << " $"
         << setw(8) << netSaleAmount << endl;

    return 0;
}
```

**Sample Run:** In this sample run, the user input is shaded.

```
Enter movie name: Journey to Mars

Enter the price of an adult ticket: 4.50

Enter the price of a child ticket: 3.00

Enter number of adult tickets sold: 800

Enter number of child tickets sold: 1850

Enter the percentage of donation: 10

-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
Movie Name: ........................ Journey to Mars
Number of Tickets Sold: ............ 2650
Gross Amount: ....................... $ 9150.00
Percentage of Gross Amount Donated: . 10.00%
Amount Donated: ..................... $ 915.00
Net Sale: ........................... $ 8235.00
```

Note that the first six lines of output get the necessary data to generate the last six lines of the output as required.

## PROGRAMMING EXAMPLE: Student Grade

Write a program that reads a student name followed by five test scores. The program should output the student name, the five test scores, and the average test score. Output the average test score with two decimal places.

The data to be read is stored in a file called `test.txt`. The output should be stored in a file called `testavg.out`.

| Input | A file containing the student name and the five test scores. A sample input is: |
| --- | --- |
| Output | The student name, the five test scores, and the average of the five test scores, saved to a file. |

```
Andrew Miller 87.50 89 65.75 37 98.50
```

### PROBLEM ANALYSIS AND ALGORITHM DESIGN

To find the average of the five test scores, you add the five test scores and divide the sum by 5. The input data is in the following form: the student name followed by the five test scores. Therefore, you must read the student name first and then read the five test scores. This problem analysis translates into the following algorithm:

- 1. Read the student name and the five test scores.
- 2. Output the student name and the five test scores.
- 3. Calculate the average.
- 4. Output the average.

You output the average test score in the fixed decimal format with two decimal places.

### Variables

The program needs to read a student's first and last name and five test scores. Therefore, you need two variables to store the student name and five variables to store the five test scores.

To find the average, you must add the five test scores and then divide the sum by 5. Thus, you need a variable to store the average test score. Furthermore, because the input data is in a file, you need an `ifstream` variable to open the input file. Because the program output will be stored in a file, you need an `ofstream` variable to open the output file. The program, therefore, needs at least the following variables:

```cpp
ifstream inFile;    //input file stream variable
ofstream outFile;   //output file stream variable

double test1, test2, test3, test4, test5; //variables to
                                          //read the five test scores
double average;     //variable to store the average test score
string firstName;   //variable to store the first name
string lastName;    //variable to store the last name
```

### MAIN ALGORITHM

In the preceding sections, we analyzed the problem and determined the formulas to perform the calculations. We also determined the necessary variables and named
