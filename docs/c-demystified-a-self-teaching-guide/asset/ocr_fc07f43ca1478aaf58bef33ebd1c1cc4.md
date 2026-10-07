# Returning a Value from a Function

Arguments are used to pass values to a called function. A return value can be used to pass a value from a called function back to the function that called it.

For example, in the previous program the functionNumbers had three arguments, the first two being the numbers to be added, the third being their sum. The following program modifies the previous by eliminating the third argument, but adding a return value to the function:

```
#include <iostream>
using namespace std;
int addNumbers(int, int);

int main () {
    int firstNum, secondNum, sum = 0;
    cout << "Enter first number: ";
    cin >> firstNum;
    cout << "Enter second number: ";
    cin >> secondNum;
    sum = addNumbers(firstNum, secondNum);
    cout << firstNum << " + " << secondNum << " = " << sum;
    return 0;
}
 addNumbers(int x, int y) {
    return x + y;
}
```

The sample input and output may be the same as in the previous program:

Enter first number: 3
Enter first number: 6
3 + 6 = 9

The return value is indicated by adding its data type, here an int, in front of the function name in both the function prototype and header:

```
int addNumbers(int, int);
addNumbers(int x, int y)
```

The function call is on the right side of the assignment operator. To the left of the assignment operator is a variable of the same data type as the return value of the function. The concept is that the return value from the function is assigned to the variable sum on the left side of the assignment operator.

```
sum = addNumbers(firstNum, secondNum);
```

The body of the function has the return keyword followed by a value of the data type compatible with the function prototype and header, here. The function’s return value is the value that follows the return keyword, here the sum of the two arguments:

```
return x + y;
```

That sum of x + y is then assigned to the variable sum in main.