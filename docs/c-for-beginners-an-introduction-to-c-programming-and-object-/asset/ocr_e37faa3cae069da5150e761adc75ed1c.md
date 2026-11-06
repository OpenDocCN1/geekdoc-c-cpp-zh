```
```cpp
{
    //This block will be executed if <condition 1> is
    false <condition 2> is true.
    <statements...>
}
else if ( <condition 3> )
{
    //This block will be executed if <condition 1>
    and <condition 2> are false and <condition 3> is
    true.
    <statements...>
}
else
{
    //This block will be executed if <condition 1>,
    <condition 2> and <condition 3> are false.
}
```
```

**Note:** If there is only one statement inside an if, else if or else block, there is no need to specify the block inside curly brackets.

Here is a simple C++ program that demonstrates the usage of if-else statements. The program accepts an integer from the user and checks if it is positive, negative or zero:

```
```cpp
#include <iostream>

using namespace std;

int main ()
{
    int i;
    int number;
    //Ask the user to enter
    cout << endl << endl
         << "Enter an integer: ";
    //Wait for user input, accept it into number variable
    cin >> number;
}
```
```