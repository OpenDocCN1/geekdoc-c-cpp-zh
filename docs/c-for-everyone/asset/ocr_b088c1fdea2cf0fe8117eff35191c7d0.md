When comparing adjacent values,\nthe store the previous value in a variable.

![](bbox=[0.54, 0.104, 0.826, 0.237])

One problem remains. When the loop is entered for the first time, previous has not yet been set. You can solve this problem with an initial input operation outside the loop:

```
double input;
double previous;
cin >> previous;
while (cin >> input)
{
    if (input == previous) { cout << "Duplicate input" << endl; }
    previous = input;
}
```

![](bbox=[0.109, 0.434, 0.258, 0.522])

# SELF CHECK

+   31. What total is computed when no user input is provided in the algorithm in Section 4.7.1?
+   
+   32. How do you compute the total of all positive inputs?
+   
+   33. What is the value of position when no match is found in the algorithm in Section 4.7.3?
+   
+   34. What is wrong with the following loop for finding the position of the first space in a string?

```
bool found = false;
for (int position = 0; !found && position < str.length(); position++)
{
    string ch = str.substr(position, 1);
    if (ch == " ") { found = true; }
}
```

+   35. How do you find the last space in a string?
+   
+   36. What is wrong with the following loop for finding the smallest input value?

```
double smallest = 0;
double input;
while (cin >> input)
{
    if (input < smallest)
    {
        smallest = input;
    }
}
```

+   37. What happens with the algorithm in Section 4.7.5 when no input is provided at all?

**Practice It**  Now you can try these exercises at the end of the chapter: P4.8, P4.13, P4.14.