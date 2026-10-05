# 9.1. FUNCTION BASICS

valalue = prompt();

assigns to the variable valueue the value indicated when the return statement executes.

Note that in Listing 9.6 (betterprompt.cpp), we declared a variable name result inside the prompt. This variable is local to the function, meaning we cannot use this particular variable outside of prompt. It also means we are free to use same name out of the prompt function in a different context, and that will not interfere with the result variable within prompt. We say that result is a local variable.

We can further enhance our prompt function. Currently prompt always sends the same message. Using parameters, we can customize the message prints. Listing 9.7 (evenprompt.cpp) shows how parameters are used to provide a customized message within prompt.

```
#include <iostream>

using namespace std;

// Definition of the prompt function
int prompt(int n) {
    int result;
    cout << "Please enter integer #" << n << ":";
    cin >> result;
    return result;
}

int main() {
    int value1, value2, sum;
    cout << "This program adds together two integers." << endl;
    value1 = prompt(1); // Call the function
    value2 = prompt(2); // Call the function again
    sum = value1 + value2;
    cout << value1 << " + " << value2 << " = " << sum << endl;
}
```

In Listing 9.7 (evenprompt.cpp), the parameter influences the message that it printed. The user is prompted to enter value #1 or value #2. The

value1 = prompt (1);

passes the value 1 to the prompt function. Since prompt's parameter is named n, the process works as if the assignment statement

n = 1;

were as the first action within prompt.

In the first line of the function definition:

int prompt (int n)

n is called the formal parameter. A formal parameter is used like a variable within the function's body, but it is declared in the function's parameter list; it is not declared in the function's body. A formal parameter is a parameter used in the formal definition of the function.