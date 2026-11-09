```
Algorithm:
1. enter the first integer, second integer, and subtraction? items
2. if subtraction?, do this:
    if the first integer is greater than the second integer
        calculate the answer by subtracting the second integer from the first integer
    otherwise, do this:
        assign the second integer to the Number 1 text box
        assign the first integer to the Number 2 text box
        calculate the answer by subtracting the first integer from the second integer
    end if
    otherwise, do this:
        calculate the answer by adding the second integer to the first integer
    end if
3. display the answer
```

instructions added to the nested selection structure's false path

Figure 10-10: First modification to the algorithm from Figure 10-6

When comparing two numbers, keep in mind that the first number can be greater than, less than, or equal to the second number. Study the comparison made in the nested selection structure’s condition in Figure 10-10. If the condition is True, it means that the first integer (entered in the Number 1 text box) is the larger of the two integers, so the answer can be calculated by subtracting the second integer from the first integer. However, if the condition is False, it doesn’t necessarily mean that the first integer (entered in the Number 1 text box) is less than the second integer (entered in the Number 2 text box); both integers could be equal. The modified algorithm in Figure 10-10 will swap the text box values, as well as calculate the answer, when the first integer is either less than or equal to the second integer. Although you could leave the algorithm as is, there is no reason to swap the text box values when both integers are equal. You can fix the algorithm by including the "equal to" comparison in the nested selection structure’s condition, as shown in the final algorithm in Figure 10-11. In the final algorithm, the nested selection structure’s condition determines whether the first integer is greater than or equal to the second integer. If the condition is True, the answer is calculated by subtracting the second integer from the first integer. If the condition is False, the text box values are swapped and the answer is calculated by subtracting the first integer from the second integer.