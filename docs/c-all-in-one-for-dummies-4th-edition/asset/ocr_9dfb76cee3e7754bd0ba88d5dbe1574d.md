retrieving the value of one variable and putting it in the other. This process is often referred to as *copying* the variable from one to another. For example, if you have two integer variables — say, `start` and `finish` — and you want to copy the value of `start` into `finish`, you would use a line of code like the following:

```
finish = start;
```

![](bbox=[0.173, 0.221, 0.239, 0.288])

Don’t let the language confuse you. Although you want to copy the value of `start` into `finish`, notice that the first thing you type is `finish`, and then the equals sign, and then `start`. The left side of the equals sign is what receives the value; it is an assignment statement.

![](bbox=[0.173, 0.302, 0.239, 0.368])

When you copy the value of one variable to another, the two variables must be the same type. You cannot, for instance, copy the value from a string variable into an integer variable. If you try, the compiler issues an error message and stops.

After the computer runs this copy statement, the two variables hold the same thing. The code for `CopyVariable`, shown in Listing 4-3, is an example of copying one variable to another.

# LISTING 4-3: Copying a Value from One Variable to Another

```
```cpp
#include <iostream>

using namespace std;

int main()
{
    int start = 50;
    int finish;
    finish = start;
    cout << finish << endl;
    return 0;
}
```
```

# Initializing a Variable

When you create a variable, it starts as an empty storage bin. Before it can be of much use, you need to put something in it.