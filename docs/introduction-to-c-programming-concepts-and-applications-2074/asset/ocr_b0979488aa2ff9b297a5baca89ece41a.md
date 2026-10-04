Program 22_10 is you with the steps to make a peanut butter and jelly sandwich.

In line 19, you have a for statement. The container, is made up of strings, so you are going to have a new value—step, in this case—is of a string type. You're going to manipulate elements of instructions, so you declare step to a string reference, not just a string. Then, there is a colon followed by the name of the container, instructions.

Then, you can have another loop through the elements of instructions, this time to print out the results. for(auto step : instructions)—says you're going to iterate through the entire container, and step is going to refer to the element of instructions on each iteration (19).

Inside the loop, when you print out the values, you see that they were changed by the previous loop (20).

Without the loop, you can do anything you want with step and it will refer the elements of the list itself. So, in this case, you are adding the step: to the beginning of each element (16). On the first iteration of the loop, then the value of element of instructions Step: added to the front. The loop ends adding this to all elements.

# READINGS

```
// Program 22_10
// Example of for-each statement
#include<iostream>
#include<string>
#include<list>
using namespace std;

int main() {
    list<string> instructions;
    instructions.push_back('Get bread');
    instructions.push_back('Put on peanut butter');
    instructions.push_back('Put two halves together');
    for (string& step : instructions) {
        step = "Step: " + step;
    }
    for (auto step : instructions) {
        cout << step << endl;
    }
}
```

+   Stroustrup, Programming Principles and Practice Using C++, chap. 20.

+   Lippman, Lajoie, and Moo, C++ Primer, sections 3.4 and 9.1-9.3.

# Exercise

Which container is the best to use in each of the following scenarios?

+   1 You're running a business and want to process orders in the same order they arrive.

+   2 You have a long sequence of directions, and you want to be able to examine any step in detail.

+   3 You are keeping track of movies you want to see in order from the ones you're most interested in least interested in. You'll be able to add new movies that you out or cross off movies once you've watched.

![](bbox=[0.448, 0.936, 0.618, 0.963])