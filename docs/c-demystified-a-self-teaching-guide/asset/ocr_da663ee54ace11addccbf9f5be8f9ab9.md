# Passing Arrays as Function Arguments

Previously in this chapter, we used the following program to demonstrate how loops are effective in assigning and displaying array values:

```
#include <iostream>
using namespace std;
const int MAX = 3;
int main ()
{
    int testScore[MAX];
    for (int i = 0; i < MAX; i++)
    {
        cout << "Enter test score #" << i << i + 1 << ":";
        cin >> testScore[i];
    }
    for (int i = 0; i < MAX; i++)
    {
        cout << "Enter test score #" << i + 1 << ":";
        cout << testScore[i] << endl;
    }
    return 0;
}
```

Now we are going to make this program more modular by writing one function to assign values to the array, and another function to display values from the array, rather than doing all work in the main function.

```
#include <iostream>
using namespace std;
void assignValues(int[], int);
void displayValues(int[], int);
const int MAX = 3;

int main ()
{
    int testScore[MAX];
    assignValues(testScore, MAX);
    displayValues(testScore, MAX);
    return 0;
}

void assignValues(int tests[], int num)
{
    for (int i = 0; i < num; i++)
    {
        cout << "Enter test score #" << i + 1 << ":";
        cin >> tests[i];
    }
}

void displayValues(int scores[], int elems)
{
    for (int i = 0; i < elems; i++)
    {
```