Note that in this case the throw statement is enclosed in a try clause. This pattern is rare.

# EXAMPLE 14.5

We repeat Program 14.3 using the *try-catch* block to see the similarity between the traditional error checking and the exception handling approach (Program 14.5). Note that exception handling in this case means ignoring only the pair of integers that caused exception and continuing with the program. Later in this chapter we see that exception handling may need other actions.

# **Program 14.5**  Using a try-catch block

```
```cpp
/*************************************************************
 * A program that uses the try-catch block to detect an error
 * and throw it to be caught and handled by the program
 *************************************************************/
#include <iostream>
using namespace std;

int main()
{
    int num1, num2, result;
    for (int i = 0; i < 3; i++)
    {
        cout << "Enter an integer: ";
        cin >> num1;
        cout << "Enter another integer: ";
        cin >> num2;
        // The try-catch block
        try
        {
            if (num2 == 0)
            {
                throw 0;       // An object of type integer is thrown
            }
            result = num1 / num2;
            cout << "The result is: " << result << endl;
        }
        catch (int x)
        {
            cout << "Division by zero cannot be performed." << endl;
        }
    }
    return 0;
}
```
```