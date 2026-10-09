# ## 1.6 Making decisions

Let's write a new program. Run through a similar process to that given above, but this time let's call our project **ExamCalculator**. Change all the folders accordingly. The code for the `main.cpp` file in this project should look like this:

```
```
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    int mark;
    cout << "What was your average mark?\n";
    cin >> mark;

    if (mark >= 70) {
        cout << "Congratulations!\n";
        cout << "You got a distinction.\n";
    }
    else if (mark >= 60) {
        cout << "Well done!\n";
        cout << "You got a merit!\n";
    }
    else if (mark >= 50) {
        cout << "You passed.\n";
    }
    else {
        cout << "You failed :-(\n";
    }

    return 0;
}
```
```

Notice first that all of the boiler plate code is the same as in the last example. This is why I'm calling it boiler plate code. You can just copy it without thinking for the time being.

The more interesting thing to notice is that we are using an `if` statement to make decisions on what the code should do next. The code to be executed in each of the different circumstances is grouped together in sets of curly brackets.

Be careful to notice the round brackets in the condition to be tested.

The `else if` parts of the statement are optional as is the `else`. You can have as many `else if` statements as you like.