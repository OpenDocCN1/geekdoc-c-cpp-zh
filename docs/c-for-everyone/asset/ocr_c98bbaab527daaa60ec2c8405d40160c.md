```
```cpp
}

// Now we know that the input is valid
int actual_floor;
if (floor > 13)
{
    actual_floor = floor - 1;
}
else
{
    actual_floor = floor;
}

cout << "The elevator will travel to the actual floor "
     << actual_floor << endl;

return 0;
}
```
```

# Program Run

```
```text
Floor: 13
Error: There is no thirteenth floor.
```
```

![](bbox=[0.109, 0.414, 0.226, 0.502])

+   36. Consider the elevator2.cpp program. What output do you get when the input is
+      a. 100?
+      b. −1?
+      c. 20?
+      d. thirteen?

37. Your task is to rewrite the elevator2.cpp program so that there is a single if statement with a complex condition:

```
```cpp
if (...)
{
    cout << "Error: Bad input" << endl;
    return 1;
}
```
```

What is the condition?

38. In the Sherlock Holmes story “The Adventure of the Sussex Vampire”, the inimitable detective uttered these words: “Matilda Briggs was not the name of a young woman, Watson, ... It was a ship which is associated with the giant rat of Sumatra, a story for which the world is not yet prepared.” Over a hundred years later, researchers found giant rats in Western New Guinea, another part of Indonesia.

Suppose you are charged with writing a program that processes rat weights. It contains the statements

```
```cpp
double weight;
cout << "Enter weight in kg: ";
cin >> weight;
```
```

What input checks should you supply?

![](bbox=[0.109, 0.847, 0.256, 0.925])