# 7.

//Lab11-1.cpp - calculates the total domestic sales,
//total international sales, and total sales
//Created/revised by <your name> on <current date>

```
#include <iostream>
using namespace std;

int main()
{
    //declare arrays and variable
    int domestic[6] = {12000, 45000, 32000,
        67000, 24000, 55000};
    int international[6] = {10000, 56000, 42000,
        23000, 12000, 34000};

    int totalSales = 0; //accumulator
    int totalDomestic = 0; //accumulator
    int totalInternational = 0; //accumulator

    for (int x = 0; x < 6; x += 1) {
        totalDomestic += domestic[x];
        totalSales += domestic[x] + international[x];
    }
    
    //display total domestic sales, total
    //international sales, and total sales
    cout << "Total domestic sales: " <<
        << totalDomestic << endl;
    cout << "Total international sales: " <<
        << totalInternational << endl;
    cout << "Total sales: " << totalSales << endl;

    system("pause");
    return 0;
}
n//end of main function
```

# 8.

//Lab11-1.cpp - calculates the total domestic sales,
//total international sales, total sales, and
//total sales made in each month
//Created/revised by <your name> on <current date>

```
#include <iostream>
using namespace std;

int main()
{
    //declare arrays and variable
    int domestic[6] = {12000, 45000, 32000,
        67000, 24000, 55000};
    int international[6] = {10000, 56000, 42000,
        23000, 12000, 34000};
```