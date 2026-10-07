# Passing as Function Arguments

Passing an array name by address is relatively simple because the value of the array name is an address. However, you may often want to pass a single variable by address. By single variable I don't mean a variable that is unmarried, but instead, for example, int as opposed to an int array.

With a single variable, subscript notation is not an option. Subscripts make sense only with an array. Rather, you need to use pointer notation to pass a single variable by address.

Passing an argument by reference or by address both enable the passed argument to be changed in the calling function—only the syntax is different. In comparison, let's test with the following program Chapter 9 that passes the variable to doubled by reference:

```
#include <iostream>
using namespace std;
void doubleIT(int&);

int main () {
    int num;
    cout << "Enter number: ";
    cin >> num;
    doubleIT(num);
    cout << "The number doubled in main is " << num << endl;
    return 0;
}

void doubleIT(int& x) {
    cout << "The number to be doubled is " << x << endl;
    x *= 2;
    cout << "The number doubled in doubleIT is " << x << endl;
}
```

Here is some sample input and output:

Enter number: 3
The number to be doubled is 3
The number doubled in doubleIT is 6
The number doubled in main is 6

Let's now modify this program so it passes the variable to be doubled by address instead of reference:

```
#include <iostream>
using namespace std;
void doubleIT(int*);
```

```
int main () {
    int num;
    cout << "Enter number: ";
    cin >> num;
    doubleIT(&num);
    cout << "The number doubled in main is " << num << endl;
    return 0;
}

void doubleIT(int* x)
```