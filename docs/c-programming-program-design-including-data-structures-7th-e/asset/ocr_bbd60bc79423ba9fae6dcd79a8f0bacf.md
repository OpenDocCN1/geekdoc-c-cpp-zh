```
```cpp
{
    int firstNum = 18;
    int secondNum = 37;

    if ((secondNum % firstNum == 2) || (secondNum % firstNum == 3))
    {
        secondNum = 3;
        firstNum = 2;
    }
    else if (secondNum % firstNum == 1)
    {
        secondNum = 18;
        firstNum = 1;
    }
    else
    {
        secondNum = 1;
        firstNum = 37;
    }

    cout << firstNum << " " << secondNum << endl;

    return 0;
}
```
```

+   18. 
+      a. What is the output of the program in Exercise 17, if `firstNum = 10` and `secondNum = 52`? (2, 3, 5)
+      b. What is the output of the program in Exercise 17, if `firstNum = 20` and `secondNum = 42`? (2, 3, 5)

19. Suppose that `sale` and `bonus` are double variables. Write an if...else statement that assigns a value to `bonus` as follows: If `sale` is greater than $20,000, the value assigned to `bonus` is 0.10, that is, 10%; if `sale` is greater than $10,000 and less than or equal to $20,000, the value assigned to `bonus` is 0.05, that is, 5%; otherwise, the value assigned to `bonus` is 0. (3)

20. Suppose that `overSpeed` and `fine` are double variables. Assign the value to `fine` as follows: If 0 < overSpeed <= 5, the value assigned to fine is $20.00; if 5 < overSpeed <= 10, the value assigned to fine is $75.00; if 10 < overSpeed <= 15, the value assigned to fine is $150.00; if overSpeed > 15, the value assigned to fine is $150.00 plus $20.00 per mile over 15. (3)

21. Suppose that `score` is an int variable. Consider the following if statements: (3)

```
```cpp
if (score >= 90)
    cout << "Discount = 10%" << endl;
```
```

+   a. What is the output if the value of `score` is 95? Justify your answer.
+   
+   b. What is the output if the value of `score` is 85? Justify your answer.