```
```cpp
#include <iostream>
using namespace std;

const int PRICE;
const long YEARS;
const double YIELD;
int main()
{
    int bondtype;
    double interest, coupon;
    .
    .
    .
    return 0;
}
double roi(int mat1, int mat2)
{
    int count;
    double effectiveRate;
    .
    .
    .
    return effectiveRate;
}
int step(double first, double last)
{
    int numofyrs;
    double fracpart;
    .
    .
    .
    return(10*numofyrs);
}
```
```

+   b. Draw a box around the appropriate section of the preceding code to enclose the scope of each variable or constant.
+   
+   c. Determine the data type of the arguments that the `roi()` and `step()` functions expect and the data type of the value these functions return.

+   2. (Practice) a. For the following section of code, determine the data type and scope of all declared variables on a separate sheet of paper, using the column headings shown in the following chart. (The entries for the first variable have been filled in.)

| Variable Name | Data Type | Scope |
|---|---|---|
| key | char | global to `main()`, `func1()`, and `func2()` |