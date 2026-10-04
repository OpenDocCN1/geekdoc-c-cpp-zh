```
// Program 3_15
```

```
// Illustrating multiple-if-else
statements
```

```
#include <iostream>
```

```
using namespace std;
```

```
int main() {
```

```
    int age = 10;
```

```
    float cost;
```

```
    if (age < 3) {
```

```
        cost = 0.0;
```

```
    }
```

```
    else {
```

```
        if (age <= 10) {
```

```
            cost = 3.0;
```

```
        }
```

```
        else {
```

```
            if (age < 17) {
```

```
                cost = 5.0;
```

```
            }
```

```
            else {
```

```
                cost = 6.0;
```

```
        }
```

```
    }
```

```
}
```

```
    cout << "Your cost is " << 
        cost << endl;
```

There's another way of using if statements that is common and useful. Suppose you have some sort of tiered pricing system, similar to the one from before, but you want kids under 3 to be free, from 3 to 5 to cost $1, from 6 to 10 to cost $3, from 11 to 17 to cost $5, and everyone else to cost $6.

Program 3_15 has a bunch of nested if statements. You start by checking whether the age is less than 3, and if so, we set a cost of 0.0. Otherwise, you go to the else clause.

In the else clause, you have another if statement, this checking whether the age is less or equal to 5. Again, you set a cost in that case; otherwise, this continues until you handle all the cases.

When you look at this code, all nested statements are confusing, especially when your conditions aren't difficult.

In these instances, it's helpful to remember that in C++, the spacing and line breaks actually matter. Thus, you can reorganize the indentation, tabs, and organization to make this more readable.

First, notice that in this situation, you have a series of else clauses, each of which contains a single statement (f).

This is the one situation where you don't use curly clauses, and not indent the if you get rid of the curly clauses when there is just another if statement inside

Notice that you still have the else if combinations, if you organize them in a way that makes it easier to see the different cases and what to do in each one. You can read the logic of conditionals and find the first one evaluates to true. Or, if not then have a final else clause. Although this is the same code it works much easier to follow. This way of organizing the code is called an else structure, and it's a good idea to use it in cases like this, where you want to select one of several options.

| else if (age <= 5) { |
| cost = 1.0; |
| } |
| else if (age <= 10) { |
| cost = 3.0; |
| } |
| else if (age <= 17) { |
| cost = 5.0; |
| } |
| else { |
| cost = 6.0; |
| } |


![](bbox=[0.277, 0.386, 0.313, 0.458])