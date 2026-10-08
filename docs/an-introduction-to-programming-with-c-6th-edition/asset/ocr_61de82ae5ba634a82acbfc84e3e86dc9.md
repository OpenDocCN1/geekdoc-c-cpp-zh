# The for Statement

4. Write a for clause that processes the loop instructions as long as the value stored in the x variable is greater than the number 0. The x variable should be an int variable. Initialize the variable to the number 25 and update it by -5 with each repetition of the loop.

5. The computer will stop processing the loop associated with the for clause from Question 4 when the x variable contains the temperature.

6. Write a for statement that displays the even integers between 2 and 9 (inclusive) on the screen. Use num as the name of the counter.

# LAB 7-1 Stop and Analyze

Study the program shown in Figure 7-42, and answer the questions. The program calculates the outside temperature.

The answers to the labs are located in Appendix A.

```
//Lab7-1.cpp - calculates the average temperature
//Created/revised by <your name> on <current date>

#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    //declare variables
    int numberOfTemps = 0; //counter
    int totalTemp = 0; //accumulator
    int temp = 0;
    double average = 0.0;

    //get first temperature
    cout << "First temperature (999 to stop): ";
    cin >> temp;

    while (temp != 999)
    {
        //update counter and accumulator
        numberOfTemps += 1;
        totalTemp += temp;
    }

//get remaining temperatures
    cout << "Next temperature (999 to stop): ";
    cin >> temp;
} //end while

//verify that at least one temperature was entered
if (numberOfTemps > 0)
```

Figure 7-42 Code for Lab 7-1 (continues)