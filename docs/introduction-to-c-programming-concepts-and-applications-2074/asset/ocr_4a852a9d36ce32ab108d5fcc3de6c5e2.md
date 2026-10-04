The commands you put in curly braces for else clause can be just any commands. That includes more if statements!

So, the code for price starts with an if statement to check whether the package is sent priority or not. There's also an else clause to handle situations when it's not priority (d).

Let's look at some code used to calculate the shipping cost for a package.

In the case where you have priority shipping, you have another if statement (e). One checks if package weight is below 3.5, it sets a fixed cost of 10.00 and otherwise assigns a cost by given weight times 3.0.

First, there's weight and type of shipping. So, you have few variables: a floating-point weight (7) and a Boolean indicator of whether is send_priority or not (8). In this case, package weight is initialized to 5.0 and sent_priority is initialized to true.

Having one if statement inside another is called nesting. It's even possible to have multiple levels of nesting.

As for cost, the system is that if there is priority shipping, all packages less than 3.5 have a fixed cost of 10.00, and otherwise the cost for priority is based on weight, while all nonpriority packages just have a cheaper cost based on weight alone.

As for the case where you don't have priority shipping, this is where the else clause of the outermost if statement comes in (19). In this case, the price is a lower rate of weight times 1.5.

You should use nesting whenever the code you have makes sense to organize in that way—where you want to make one choice and another.

```
// Program 3_14
// Illustrating nested if statement
#include <iostream>
using namespace std;
int main() {
    float package_weight = 5.0;
    bool send_priority = true;
    float price;
    if (send_priority) {
        if (package_weight < 3.5) {
            price = 10.00;
        }
    } else {
            price = package_weight * 1.5;
    }
    cout << "Your price is " << price << endl;
}
```