# FIGURE 2.2 Sample Program for the Throttle Class

# A Program

```
// FILE: demo1.cxx
// This small demonstration shows how the throttle class is used.
#include <iostream>     // Provides cout and cin
#include <cstdlib>      // Provides EXIT_SUCCESS
using namespace std;    // Allows all Standard Library items to be used
class throttle
{
public:
    // MODIFICATION MEMBER FUNCTIONS
    void shut_off( );
    void shift(int amount);
    // CONSTANT MEMBER FUNCTIONS
    double flow( ) const;
    bool is_on( ) const;
private:
    int position;
};
int main( )
{
    throttle sample;
    int user_input;
    // Set the sample throttle to a position by the user.
    cout << "I have a throttle with 6 positions." << endl;
    cout << "Where would you like to set the throttle? " << endl;
    cout << "Please type a number from 0 to 6: ";
    cin >> user_input;
    sample.shut_off( );
    sample.shift(user_input);
    // Shift the throttle down to zero, printing the flow along the way.
    while (sample.is_on( ))
    {
        cout << "The flow is now " << sample.flow( ) << endl;
        sample.shift(-1);
    }
    cout << "The flow is now off" << endl;
    return EXIT_SUCCESS;
}
```

These lines are the definition of the throttle class.

This is the declaration of a throttle object called sample.

In the actual program, you would place the implementations of the throttle's four member functions here, but we haven't yet written these implementations!