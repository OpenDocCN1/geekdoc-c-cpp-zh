# Mini-Quiz 11-3

+   1. Write a C++ if clause that determines whether the value stored in the prices[x] variable is less than the lowest variable. The array and variable have the double data type.

+   2. The process of arranging data in alphabetical or numerical order is called

+   3. Write a for loop that counts the number 3 from each of the 10 elements in an int array name orders. Use a variable named x to keep track of the array subscripts. Initialize the x to 0.

> The answers to Mini-Quiz questions are located in Appendix A.

# LAB 11-1 Stop and Analyze

Study the program in Figure 11-55, and then answer the questions. The domestic array contains the company sold domestically during the months of January through June. The international array contains the company sold internationally during the same period.

> The answers to the labs are located in Appendix A.

```
//Lablab11-1.cpp - calculates the total sales
//Created/revised by <your name> on <current date>

#include <iostream>
using namespace std;
int main() {
    //declare arrays and variable
    int domestic[6] = (12000, 45000, 32000,
    67000, 24000, 55000);
    int international[6] = (10000, 56000, 42000,
    23000, 56000, 34000);
    int totalSales = 0;
    //accumulate sales
    for (int x = 0; x < 6; x += 1)
        totalSales += domestic[x] + international[x];
    //end for

    //display total sales
    cout << "Total sales: " << totalSales << endl;
    system("pause");
    return 0;
} //end of main function
```

Figure 11-55 Code for Lab 11-1