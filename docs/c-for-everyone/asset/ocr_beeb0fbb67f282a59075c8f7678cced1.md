```
```cpp
36      cout << " <= largest value";
37    }
38    cout << endl;
39  }
40
41    return 0;
42 }
```
```

# Program Run

```
```
Please enter values, Q to quit:
34.5 80 115 44.5 Q
34.5
80
115 <= largest value
44.5
```
```

![](bbox=[0.077, 0.332, 0.222, 0.418])

# SELF CHECK

8. What is the output of the largest.cpp program with the following inputs?

```
```
20 10 20 Q
```
```

9. Write a loop that counts how many elements in an array are equal to zero.

10. Consider the algorithm to find the largest element in an array. Why don’t we initialize largest and it with zero, like this:

```
```cpp
double largest = 0;
for (int i = 0; i < size of values; i++)
{
    if (values[i] > largest)
    {
        largest = values[i];
    }
}
```
```

11. When printing separators, we skipped the separator before the initial element. Rewrite the loop so that the separator is printed after each element, except for the last element.

12. What is wrong with these statements for printing an array with separators?

```
```cpp
cout << values[0];
for (int i = 1; i < size of values; i++)
{
    cout << ", " << values[i];
}
```
```

13. When searching for a match, we used a while loop, not a for loop. What is wrong with using this loop instead?

```
```cpp
for (pos = 0; pos < size of values && !found; pos++)
{
    if (values[pos] == 100)
    {
        found = true;
    }
}
```
```

14. When inserting an element into an array, we moved the elements with larger index values, starting at the end. Why is it wrong to start at the insertion location, like this: