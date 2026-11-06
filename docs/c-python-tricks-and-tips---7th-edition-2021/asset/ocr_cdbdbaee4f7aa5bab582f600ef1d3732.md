# If… Else Statement

There is a much better way to use an if statement in your code, with if… else. If… else works in much the same way as a standard if statement. If the Boolean expression is true, the code within the braces is executed. Else, the code within the next set of braces is used instead.

# IF YES, ELSE NO

There are two sections of code that can be executed depending on the outcome in an if… else statement. It’s quite easy to visualise once you get used to its structure.

STEP 1 — Begin with a new C++ file and the standard headers:

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
}
```
```

![](bbox=[0.252, 0.412, 0.491, 0.49])

STEP 2 — Let’s expand the code from the If Statement on the previous page:

```
```cpp
{
    int num = 1;

    if ( num < 30 )
    {
        cout << “The number is less than 30!” << endl;
    }
    else
    {
        cout << “The number is greater than 30!” << endl;
    }

    return 0;
}
```
```

![](bbox=[0.066, 0.771, 0.491, 0.927])

STEP 3 — The first line in the code creates the integer called num and gives it a value of 1. The if statement checks to see if the value of num is less than thirty and if it is it outputs “The number is less than 30!” to the console.

```
```cpp
if ( num < 30 )
{
    cout << "The number is less than 30!" << endl;
}
```
```

STEP 4 — The else companion to if checks if the number is greater than 30 and if so, then displays “The number is greater than 30!” to the console; and finally, the code is terminated satisfactorily.

```
```cpp
}
else
{
    cout << "The number is greater than 30!" << endl;
}
```
```

STEP 5 — You can change the value of num in the code or you can improve the code by asking the user to enter a value:

```
```cpp
{
    int num;

    cout << “Enter a number: “;
    cin >> num;

    if ( num < 30 )
    {
        cout << “The number is less than 30!” << endl;
    }
    else
    {
        cout << “The number is greater than 30!” << endl;
    }

    return 0;
}
```
```