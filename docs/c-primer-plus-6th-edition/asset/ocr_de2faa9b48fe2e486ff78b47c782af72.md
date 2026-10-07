# Time on Our Hands: Developing an Operator Overloading Example

But making the method operator() also lets you use operator notation:
total = coding + fixing; // operator notation

Either notation invokes the operator(). Note that with the operator notation, the object to the left of the operator (coding, in this case) is the invoking object, and the object to the right (fixing, in this case) is the one passed as an argument. Listing 11.6

# Listing 11.6 usetime.cpp

```
// usetime.cpp -- using the second draft of the Time class
// compile usetime.cpp and mytetime.cpp together
#include <iostream>
#include "mytime.h"

int main()
{
    using std::cout;
    using std::endl;
    Time planning;
    Time coding(2, 40);
    Time fixing(5, 55);
    Time total;

    cout << "planning time = ";
    planning.Show();
    cout << endl;

    cout << "coding time = ";
    coding.Show();
    cout << endl;

    cout << "fixing time = ";
    fixing.Show();
    cout << endl;

    total = coding + fixing;
    // operator notation
    cout << "coding + fixing = ";
    total.Show();
    cout << endl;

    Time morefixing(3, 28);
    cout << "more fixing time = ";
    morefixing.Show();
    cout << endl;
    total = morefixing.operator+(total);
```