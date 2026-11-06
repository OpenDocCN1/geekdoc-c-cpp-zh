# 4.7.3 **Finding the First Match**

If your goal is to find a match, exit the loop when the match is found.

When you count the values that fulfill a condition, you need to look at all values. However, if your task is to find a match, then you can stop as soon as the condition is fulfilled.

Here is a loop that finds the first space in a string. Because we do not visit all elements in the string, a while loop is a better choice than a for loop:

```
```cpp
bool found = false;
int position = 0;
while (!found && position < str.length())
{
    string ch = str.substr(position, 1);
    if (ch == " ") { found = true; }
    else { position++; }
}
```
```

![](bbox=[0.642, 0.128, 0.924, 0.297])

*When searching, you look at items until a match is found.*

If a match is found, then found is true and position is the index of the first match. If the loop did not find a match, then found remains false after the end of the loop.

In the preceding example, we searched a string for a character that matches a condition. You can apply the same process for user input. Suppose you are asking a user to enter a positive value < 100. Keep asking until the user provides a correct input:

```
```cpp
bool valid = false;
double input;
while (!valid)
{
    cout << "Please enter a positive value < 100: ";
    cin >> input;
    if (0 < input && input < 100) { valid = true; }
    else { cout << "Invalid input." << endl; }
}
```
```

Note that the variable input is declared outside the while loop because you will want to use the input after the loop has finished. If it had been declared inside the loop body, you would not be able to use it outside the loop.

# 4.7.4 **Maximum and Minimum**

To find the largest value, update the largest value seen so far whenever you see a larger one.

To compute the largest value in a sequence, keep a variable that stores the largest element that you have encountered, and update it when you find a larger one:

```
```cpp
double largest;
cin >> largest;
double input;
while (cin >> input)
{
    if (input > largest)
    {
        largest = input;
    }
}
```
```

This algorithm requires that there is at least one input.