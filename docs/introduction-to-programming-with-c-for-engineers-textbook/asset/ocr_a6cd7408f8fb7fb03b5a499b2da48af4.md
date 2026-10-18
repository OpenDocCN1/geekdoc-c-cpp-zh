```
```cpp
using std::cout, std::cin, std::endl;

int main()
{
    // This program computes the compound interest rate
    cout << "Enter the initial amount to invest: " << endl;
    double C_0 {};    // Initial amount
    cin >> C_0;
    if(C_0 <= 0.0 )
    {
        cout << "Wrong value, exiting..." << endl;
        return -1;
    }
}
```
```

On lines [1] and [2], two header files from C++ libraries are included. Thanks to this, we can use the already mentioned std::pow function, as well as the std::cout and std::cin objects representing the output screen and the input keyboard, respectively. To avoid repeating the std:: prefix over and over again, on line [5], the names of the input-output objects from the std namespace are introduced with the help of the using directive (see Section 3.5).

Line [9] begins defining the main function. C++ applications are required to contain exactly one definition of main. Further details of various forms of main are presented in Appendix A.2.2.

On line [12], we output text on the screen using the cout object, the << operator, as well as a text constant in quotation marks. (We will see that the action of an operator such as << can differ, depending on the types of objects it is used to act on.) endl means to move the cursor to the next line and update the screen.

On line [13], a variable named C_0 is created to hold an initial amount. The names of variables are very important for conveying useful information. So, this variable could be named something like initial_amount. However, when implementing equations, such as Eq. (2.3), it is usually better to keep the names of the equation’s elements; and mathematical equations are usually written with single letters and subscrips. The variable (object) C_0 can hold any positive value, including fractions. Because of this, double was chosen for its type. C_0 is created and, on the same line immediately initialized to 0 by typing {}.

Next, on line [14], we wait for the user to enter the real value of the initial capital. After that, we check this value on line [16]. If it is not correct, the program writes out a message and, on line [19], the error code -1 is returned. Checking for incorrect values is one of the very important, but frequently forgotten, actions that need to be performed in real code - always try to stay on the safe side. In C++, there are more advanced mechanisms to deal with errors than returning an error code; these are discussed in Section 3.13.2.5.