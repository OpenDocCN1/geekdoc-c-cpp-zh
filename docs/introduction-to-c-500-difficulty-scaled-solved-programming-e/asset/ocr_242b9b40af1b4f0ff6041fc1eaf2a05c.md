are equivalent to:

```
bool a = (b and c) or not d;
int a = (b bitand c) bitor compl d;
```

My preference is to use the operators.

Although we'll discuss about the if statement in the next chapter, we'll use it in some of the following programs so that you can better understand the use of the operators.

# EXERCISES

C.4.4 Write a program that reads an integer and displays a message to indicate whether it is even or odd.

Use the & operator.

```
#include <iostream>
using std::cout;
using std::cin;

int main() {
    int num;
    cout << "Enter number: ";
    cin >> num;

    if(num & 1) == 1) // We could also write if(num & 1)
        cout << "The number " << num << " is odd\n";
    else
        cout << "The number " << num << " is even\n";
    return 0;
}
```

Comments: To determine whether a number is even or odd we check its last digit. If it is 0, it is even; otherwise, it is odd. Suppose the variable num is coded in binary as:

xxxxxxxxxxxx xxxxxxxxxx

where each '&' represents a bit of 0 or 1. Then, the result of num & 1 is:

```
xxxxxxxx xxxxxxxxxx xxxxxxxx
00000000 00000000 00000000 00000001
00000000 00000000 00000000 00000000
```

Therefore, the result is equal to the value of the last bit. If it is 1, the condition in the if statement is true and the program displays a message that the number is odd. If it is 0, the condition is false and the program displays a message that the number is even.

Notice that this solution is based on the assumption we've made in Chapter 2 that the system uses the most common method to represent negative numbers, that is, the two's complement. For a more generic and portable solution, you should use the % operator.