# Reviewing Passing Variables by Value

Recall that, unless you specify otherwise, variables are passed by value in C++. This means the computer passes only a copy of the variable's contents to the receiving function. When only a copy of the contents is passed, the receiving function is not access to the variable in memory. Therefore, it cannot change the value stored inside the function. It is appropriate to pass a variable by value when the receiving function knows the variable's contents, but does not need to change them. To illustrate, consider the C++ program shown in Figure 10. The program defines and calls a function named displayAge (on Lines 24 through 27). Therefore, the program includes an appropriate function prototype (on Line 8). The displayAge function is a void function, with its call (on Line 17) as a statement. The function passes the age by value to the displayAge function. Notice that the data type of the actual argument in the function header—int—matches the data type of the formal parameter listed in the function prototype. Also note that the name of the actual argument (years) differs. To avoid confusion, it is better to use different names for an argument and its corresponding function parameter.

> The receiving function can change only its copy of a passed value. Changing the value does not change the contents of the original.

```
//Age.cpp displays the user's age in a message
//Created/revised by <name> on <current date>

#include <iostream>
using namespace std;

//function prototype
void displayAge(int years);

int main() {
    int age = 0;
    //get age
    cout << "How old are you";
    cin >> age;
    //display age
    displayAge(age);
    return 0;
}//end of main function

****function definitions****
void displayAge(int years) {
    cout << "You are " << age << " years old." << endl;
}//end of displayAge function
```

Figure 10-5 Age message program