```
```cpp
case 5:
case 7:
    cout << "Odd";
    break;
}
```
```

27. Suppose that score is an int variable. Consider the following C++ code: (3, 11)

```
```cpp
int score;
cin >> score;
switch (score % 7)
{
case 0:
    score = score / 2 - 1;
    break;
case 1: case 3:
    score = 3 * score + 1;
    break;
case 2:
    ++score;
    break;
case 4:
    break;
case 5: case 6:
    score = score % 3;
    break;
default:
    score = score / 2;
}
cout << score << endl;
```
```

+   a. What is the output if the input is 12?
+   
+   b. What is the output if the input is 4?
+   
+   c. What is the output if the input is 3?
+   
+   d. What is the output if the input is 25?

28. Suppose that beta is an int variable. Consider the following C++ code: (11)

```
```cpp
cin >> beta;
switch (beta % 8)
{
case 0:
case 1:
    beta = beta + beta;
    break;
case 2:
    beta--;
    break;
case 3:
case 7:
    beta = static_cast<int>(sqrt(beta * 1.0));
    beta = beta / 3;
    break;
```
```

![](bbox=[0.913, 0.28, 1.0, 0.387])