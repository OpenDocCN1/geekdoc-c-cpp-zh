# 11.1. VECTORS

The general form of this range-based for statement is

```
for ( type elementvariable : vectorvariable ) statement using elementvariable
```

If the element variable within the range-based for loop is declared to be a reference, the code within the body of the loop may modify the vector's elements. Listing 11.5 (foreachexample.cpp) allows a user to populate a vector with 10 numbers and then prints the vector's contents.

# Listing 11.5: foreachexample.cpp

```
#include <iostream>
#include <vector>
using namespace std;
int main() {
    // Declare a vector of ten numbersn    vector<double> vec(10);

    // Allow the user to populate the vector
    cout << "Please enter 10 numbers: " << vec;
    for (double& elem : vec) {
        cin >> elem;
    }\

    // Print the vector's contents
    for (double& elem : vec) {
        cout << elem << endl;
    }
}
```

Note that the range-based for statement in Listing 11.5 (foreachexample.cpp) uses a reference to assign each element to the vector. The second range-based for statement does not need to use a reference variable because it is not possible to change any of the contents of vector variable. The range-based for statement iterates forward through the vector elements and cannot move backwards. The range-based statement is not convenient if you want to consider only a portion of the elements in the vector. Examples include visiting every element in the vector or considering only the first third of the elements. In these specialized cases a standard for loop with an integer counter is the better choice.

# 11.1.3 Vector Methods

A vector is, and objects differ from the simple types like int, double, and bool, in a number of ways. Most objects have access to special functions called methods. C++ programmers often offer methods as member functions. A method is a function associated with a class of objects. A method invocation involves a slightly different syntax than a function; for example, if obj is an object that supports a method named f that accepts no parameters, you can invoke f on obj with the statement:

```
obj.f();
```