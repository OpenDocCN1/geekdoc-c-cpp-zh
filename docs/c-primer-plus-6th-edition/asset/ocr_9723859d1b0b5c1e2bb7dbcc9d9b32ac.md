# Functions 57

object names are not keywords. However, using the same name, say cout for both an object and a variable in a program confuses the compiler. That is, you can use cout as a variable name in a function that doesn't use the cout object for output, but you can't use both ways in the same function.

# Using a User-Defined Function That Has a Return Value

Let's go one step further and write a function that uses the return statement. The main() function already illustrates the plan for a function with a return value: Give the return type in the function header and return at the end of the function body. You can use this form to solve a weighty problem for visiting the United Kingdom. In the United Kingdom, many bathroom scales are calibrated in stone instead of U.S. pounds or international kilograms. The word stone is singular and plural in this context. (The English language lacks the internal consistency of, say, C++) One is 14 pounds, and the program in Listing 2.6 uses a function to make this conversion.

# Listing 2.6 convert.cpp

```
// convert.cpp -- converts stone to pounds
#include <iostream>
int stonolb(int);      // function prototype
int main()
{
    using namespace std;
    int stone;
    cout << "Enter the weight in stone: ";
    cin >> stone;
    int pounds = stonolb(stone);
    cout << stone << " stone = ";
    cout << pounds << " pounds." << endl;
    return 0;
}

int stonolb(int sts)
{
    return 14 * sts;
}
```

Here's a sample run of the program in Listing 2.6:
Enter the weight in stone: 15
15 stone = 210 pounds.

In main(), the program uses cin to provide a value for the integer variable stone. This value is passed to the stonolb() function as an argument and is assigned to the variable sts in that function. stonolb() then uses the return keyword to return the value of 14 * sts to main(). This illustrates that you aren't limited to following return with a simple number. Here, by using a more complex expression, you avoid the bother of having