
## PROBLEM ANALYSIS AND ALGORITHM

To calculate the amount donated to the local charity and the net sale, you first need to determine the gross amount. To calculate the gross amount, you multiply the number of adult tickets sold by the price of an adult ticket, multiply the number of child tickets sold by the price of a child ticket, and then add these two numbers. That is:

```
grossAmount = adultTicketPrice * noOfAdultTicketsSold
              + childTicketPrice * noOfChildTicketsSold;
```

Next, you determine the percentage of the amount donated to the charity and then calculate the net sale amount by subtracting the amount donated from the gross amount. The formulas to calculate the amount donated and the net sale amount are given below. This analysis leads to the following algorithm:

- 1. Get the movie name.
- 2. Get the price of an adult ticket.
- 3. Get the price of a child ticket.
- 4. Get the number of adult tickets sold.
- 5. Get the number of child tickets sold.
- 6. Get the percentage of the gross amount donated to the charity.
- 7. Calculate the gross amount using the following formula:

    ```
    grossAmount = adultTicketPrice * noOfAdultTicketsSold
                  + childTicketPrice * noOfChildTicketsSold;
    ```

- 8. Calculate the amount donated to the charity using the following formula:

    ```
    amountDonated = grossAmount * percentDonation / 100;
    ```

- 9. Calculate the net sale amount using the following formula:

    ```
    netSaleAmount = grossAmount - amountDonated;
    ```

## VARIABLES

From the preceding discussion, it follows that you need variables to store the movie name, adult ticket price, child ticket price, number of adult tickets sold, number of child tickets sold, percentage of the gross amount donated to the charity, gross amount, amount donated, and net sale amount. Therefore, the following variables are needed:

```cpp
string movieName;
double adultTicketPrice;
double childTicketPrice;
int noOfAdultTicketsSold;
int noOfChildTicketsSold;
double percentDonation;
double grossAmount;
double amountDonated;
double netSaleAmount;
```

Because `movieName` is declared as a `string` variable, you need to include the header file `string`. Therefore, the program needs, among others, the following include statement:

```cpp
#include <string>
```

## Formatting Output

In the output, the first column is left-justified and the numbers in the second column are right-justified. Therefore, when printing a value in the first column, the manipulator `left` is used; before printing a value in the second column, the manipulator `right` is used. The empty space between the first and second columns is filled with dots; the program uses the manipulator `setfill` to accomplish this goal. In the lines showing the gross amount, amount donated, and net sale amount, the space between the `$` sign and the number is filled with blank spaces. Therefore, before printing the dollar sign, the program uses the manipulator `setfill` to set the filling character to blank. The following statements accomplish the desired output:

```cpp
cout << "*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*"
     << "*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*" << endl;
cout << setfill('.') << left << setw(35) << "Movie Name: "
     << right << " " << movieName << endl;
cout << left << setw(35) << "Number of Tickets Sold: "
     << setfill(' ') << right << setw(10)
     << noOfAdultTicketsSold + noOfChildTicketsSold
     << endl;
cout << setfill('.') << left << setw(35) << "Gross Amount: "
     << setfill(' ') << right << " $" 
     << setw(8) << grossAmount << endl;
cout << setfill('.') << left << setw(35)
     << "Percentage of Gross Amount Donated: "
     << setfill(' ') << right
     << setw(9) << percentDonation << '%' << endl;
cout << setfill('.') << left << setw(35) << "Amount Donated: "
     << setfill(' ') << right << " $"
     << setw(8) << amountDonated << endl;
cout << setfill('.') << left << setw(35) << "Net Sale: "
     << setfill(' ') << right << " $"
     << setw(8) << netSaleAmount << endl;
```

## MAIN ALGORITHM

In the preceding sections, we analyzed the problem and determined the formulas to do the calculations. We also determined the necessary variables and named constants. We can now expand the previous algorithm to solve the problem given at the beginning of this programming example.

- 1. Declare the variables.
- 2. Set the output of the floating-point numbers to two decimal places in a fixed decimal format with a decimal point and trailing zeros. Include the header file `iomanip`.

```cpp
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

        cout << "Enter the price of a child ticket: ";  //Step 7
        cin >> childTicketPrice;                          //Step 8
        cout << endl;

        cout << "Enter the number of adult tickets "
             << "sold: ";                                //Step 9
        cin >> noOfAdultTicketsSold;                      //Step 10
        cout << endl;

        cout << "Enter the number of child tickets "
             << "sold: ";                                //Step 11
        cin >> noOfChildTicketsSold;                      //Step 12
        cout << endl;

        cout << "Enter the percentage of donation: ";    //Step 13
        cin >> percentDonation;                           //Step 14
        cout << endl;

                    //Step 15
        grossAmount = adultTicketPrice * noOfAdultTicketsSold +
                      childTicketPrice * noOfChildTicketsSold;

                    //Step 16
        amountDonated = grossAmount * percentDonation / 100;

        netSaleAmount = grossAmount - amountDonated;      //Step 17

        //Step 18: Output results
        cout << "-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*"
             << "-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*" << endl;
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

```text
Enter movie name: Journey to Mars

Enter the price of an adult ticket: 4.50

Enter the price of a child ticket: 3.00

Enter number of adult tickets sold: 800

Enter number of child tickets sold: 1850

Enter the percentage of donation: 10

.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.
Movie Name: ................... Journey to Mars
Number of Tickets Sold: ........ 2650
Gross Amount: ................... $ 9150.00
Percentage of Gross Amount Donated: 10.00%
Amount Donated: ................. $ 915.00
Net Sale: ....................... $ 8235.00
```

Note that the first six lines of output get the necessary data to generate the last six lines of the output as required.
