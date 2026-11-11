
```text
-1
Invalid Day Number
End of the program
```

## Quiz

- 1. Translate the given `if-else` construct into a switch statement  
  (Assume variable x is of type integer)

    ```c
    if (x > 1000)
    {
        printf("Condition is true\n");
    }
    else
    {
        printf("Condition is false\n");
    }
    ```

- 2. What is the output of the following code? (Choose the correct option)

    ```c
    #include<stdio.h>
    void main()
    {
        if (NULL)
        {
            printf("Inside the if block \n");
        }
        printf("Outside the if block\n");
    }
    ```

  - (a) This is a compilation error
  - (b) This is a runtime error
  - (c) Output is:
    ```text
    Inside the if block
    Outside the if block
    ```
  - (d) Output is:
    ```text
    Outside the if block
    ```

- 3. What is the output of the following code? (Choose the correct option)

    ```c
    #include<stdio.h>
    void main()
    {
        int a = 25;
        if (a)
        {
            printf("Inside the if block \n");
        }
        printf("Outside the if block\n");
    }
    ```

  - (a) This is a compilation error
  - (b) This is a runtime error
  - (c) Output is:
    ```text
    Inside the if block
    Outside the if block
    ```
  - (d) Output is:
    ```text
    Outside the if block
    ```

- 4. Translate the given if-else construct using a conditional operator `?:`  
  (Assume a, b and c are integer type variables defined in the program)

    ```cpp
    if (a > b)
    {
        printf("Condition 1 is true\n");
        if (b > c)
        {
            printf("Condition 2 is true\n");
        }
        else
        {
            printf("Condition 2 is false\n");
        }
    }
    else
    {
        printf("Condition 1 is false\n");
    }
    ```

- 5. What is the output of the following code? (Choose the correct option)

    ```cpp
    #include<stdio.h>
    void main()
    {
        int x = 10, y = 20, z = 30;
        if ((++x > y && y++ < z--))
        {
            printf("The condition is true\n");
        }
        else
        {
            printf("The condition is false\n");
        }
    }
    ```

  - (a) This is a compilation error
  - (b) This is a runtime error
  - (c) Output is:
    ```text
    The condition is true
    ```
  - (d) Output is:
    ```text
    The condition is false
    ```

- 6. What is the output of the following code

    ```c
    #include<stdio.h>
    void main()
    {
        int a = 55, b = 90, c = 81, d = 22, r;
        r = a > b && c > d ? a > c ? c < d ? a : b : c : d;
        printf("Result is %d\n", r);
    }
    ```

### Error Finding Exercise

Given below are some programs which may or may not contain errors. Correct the error(s) if exist in the code and determine the output.

**Program_1**

```c
#include<stdio.h>
void main()
{
    int a = NULL;
    if (printf("Value of a is %d\n", a))
    {
        printf("Inside the if block\n");
    }
    else
    {
        printf("Inside the else block\n");
    }
    printf("End of the code\n");
}
```

**Program_2**

```c
#include<stdio.h>
void main()
{
    if ("A" >> "B")
    {
        printf("A is greater than B\n");
    }
    else
    {
        printf("A is not greater than \n");
    }
}
```

**Program 3**

```c
#include<stdio.h>
void main()
{
    int a, b, c;
    printf("Enter the values of a b\n");
    scanf("%d %d", &a, &b);
    if (c = a > b > NULL ? NULL : -1 : -2);
    {
        printf("Condition is true\n");
    };
    else
    {
        printf("Condition is false \n");
    };
}
```

**Program 4**

```c
#include<stdio.h>
void main()
{
    int x = 10, y = 20, z = 30;
    if (x < y > z > 10 > 20 < 30)
    {
        printf("The condition is true\n");
    }
    else
    {
        printf("The condition is false\n");
    }
}
```

**Program 5**

```c
#include<stdio.h>
void main()
{
    int a, b, c;
    printf("Enter the values of a b\n");
    scanf("%d %d", &a, &b);
    if (a = b == b)
    {
        printf("TRUE\n");
    }
    else
    {
        printf("FALSE\n");
    }
}
```

### Review Questions

- 1. Explain a need of decision making control statements in the program with an example.
- 2. Write a short note on the else-if ladder in C/C++. Compare if-else construct with the else-if ladder using an example of your choice.
- 3. Write a program to take a character as input from the user and to check if it's a vowel or not. The program should recognize vowel characters in upper as well as lower case.
- 4. Write a program to find the greatest of five numbers using a decision making operator(?:
- 5. Explain the use of switch statement with an example.
- 6. Write a program to show the usage of goto statement. Write a program to print a message "Hello World" n times using if construct and a goto statement (where n is the value to be taken as input from the user).
- 7. Write a program to take a month number as input from the user and to print the name of the month. For example, if user inputs a value 2 the program must print February. Make use of switch statement.
- 8. Write a program to take a number as input from the user and to determine if the number is even or odd using switch statement
- 9. Write a program to take the year as input from the user and to check if it's a leap year or not.

## Chapter 5

## Iterative Control Statements: Loops

### 5.1 Introduction

Often we come across requirements where same set of operations need to be executed multiple times to generate the required output. For example, we need to repeatedly perform multiplication to calculate factorial of a number; we need to repeatedly draw lines to construct a polygon and so on. Each time the operation may use different data sets for evaluation; hence, results of each of the individual operations may be different, but the expression that defines the operation is always the same. To give an example, although lines are drawn repeatedly to construct a polygon, the [x, y] coordinates (data values) giving start and end of a line may be different each time. Immaterial of the data used in each stage, we will still consider this as an repetitive execution of the same operation. We can form an expression to draw line from (x1, y1) to (x2, y2) in terms of variables x1, y1, x2 and y2. We can change the value of these variables each time before repeating draw line operation so as to ensure that each line is created at a different position and the consolidated result is a polygon.

To elaborate what we just said, let us try to construct a triangle using a series of drawLine operations. A triangle can be visualized as a consolidated effect of three lines drawn at correct positions. Hence, the execution of the drawLine operation must be repeated thrice. Before we proceed further, readers are requested to note that the detailed study of computer graphics is out of the scope of this textbook, however, we still give an example to draw a triangle using some abstract operation drawLine to understand the concept of loops in C/C++.

Let us assume that the expression to draw a single line from point (x1, y1) to point (x2, y2) be as shown below:

`drawLine[(x1,y1),(x2,y2)]`

Drawing a triangle using this operation will now be a three-step process, which is elaborated as below:

**Stage 1:** Initialize variables x1=50, y1=0, x2=0, y2=50 and execute the operation

`drawLine[(x1,y1),(x2,y2)]`

The line drawn in this step is shown in Figure 5.1.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_162_0.png)

**Figure 5.1:** Output after first drawLine operation

**Stage 2:** Initialize variables x1=50, y1=0, x2=100, y2=50 and again execute the operation

`drawLine[(x1,y1),(x2,y2)]`

The line drawn in this step is shown in Figure 5.2.

**Stage 3:** Initialize variables x1=0, y1=50, x2=100, y2=50 and again execute the operation

`drawLine[(x1,y1),(x2,y2)]`

The line drawn in this step is shown in Figure 5.3.

Note that in all the three stages we repeat the following expression:

`drawLine[(x1,y1),(x2,y2)]`

However, the data used in each stage is different (the actual values of variables x1, x2, y1, and y2 are different at each stage). When working with loops, our focus should be in understanding

![](img/57c0d966bb33c67a5a188e6bf39e4e02_162_1.png)

![](img/57c0d966bb33c67a5a188e6bf39e4e02_162_2.png)

**Figure 5.2:** Output after second drawLine operation

**Figure 5.3:** Output after third drawLine operation
