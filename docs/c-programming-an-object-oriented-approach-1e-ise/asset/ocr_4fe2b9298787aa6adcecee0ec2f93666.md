# **Program 9.15** Finding the Pascal coefficients

```
```cpp
/**************************************************************
 * The program shows how to create Pascal coefficients using  *
 * a ragged array dynamically allocated on the heap.           *
 **************************************************************/
#include <iostream>
#include <iomanip>
using namespace std;

int main ()
{
    // Declaration
    int maxPower = 10;
    int n;
    // Input validation
    do
    {
        cout << "Enter the power of binomial: ";
        cin >> n;
    } while (n < 0 || n > maxPower);
    // Allocate memory from heap
    int** pascal = new int* [n + 1];
    for (int i = 0; i < n + 1; i++)
    {
        pascal[i] = new int [i];
    }
    // Formation of the coefficient
    for (int i = 0; i <= n; i++)
    {
        for (int j = 0; j < i + 1; j++)
        {
            if (j == 0 || j == i)
            {
                pascal[i][j] = 1;
            }
            else
            {
                pascal[i][j] = pascal[i - 1][j - 1] + pascal[i - 1][j];
            }
        }
    }
    // Print coefficients
    cout << endl;
    cout << "Coefficients for (x + y)^" << n << " are:";
    for (int j = 0; j <= n; j++)
```
```