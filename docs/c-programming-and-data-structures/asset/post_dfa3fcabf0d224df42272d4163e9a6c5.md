
### EXAMPLE 1.7 Draw a flowchart for the problem statement given in Example 1.2.

**Solution**

![](img/fe6da5f61b1e2c77309bbee135b45e35_45_0.png)

**Fig. 1.40** *Flowchart to find the average of marks obtained by a student*

### EXAMPLE 1.8 Draw a flowchart for the problem statement given in Example 1.3.

**Solution**

![](img/fe6da5f61b1e2c77309bbee135b45e35_45_1.png)

**Fig. 1.41** *Flowchart to determine whether the given year is a leap year or not*

Introduction to Computers, Problem Solving and Basic C 1.35

### EXAMPLE 1.9 Draw a flowchart for the problem statement given in Example 1.4.

**Solution**

```text
Start
Read num
Is (num%2)=0?
No
Yes
Display "Even Number"
Display "Odd Number"
Stop
```

**Fig. 1.42** Flowchart to find out whether a given number is even or odd

### EXAMPLE 1.10 Draw a flowchart for the problem statement given in Example 1.5.

**Solution**

![](img/fe6da5f61b1e2c77309bbee135b45e35_47_0.png)

**Fig. 1.43** Flowchart to determine whether a given string is a palindrome or not

## 1.11 PSEUDOCODES

Analyzing a detailed algorithm before developing a program is very time consuming. Hence, there arises a need of a specification that only focuses on the logic of the program. Pseudocodes serve this purpose by specifying only the logic, which is used by the programmer for developing a computer program. Pseudocode is not written using specific syntax of a programming language rather it is written with a combination of generic syntax and normal English language. It helps the programmer understand the basic logic of the program after which it is the programmer's choice to write the final code in any programming language.

```text
DEFINE Integer num1, num2, result
READ Integer num1
READ Integer num2
SET result = num1 + num2
Display result
```

**Fig. 1.44** Pseudocode to add two numbers and display the result

After the pseudocode for a computer program has been written, it is used to develop the source code for the computer program. The source code is developed using a programming language, which can be an assembly language or a high level programming language.

### 1.11.1 Pseudocode Rules

- Instruction or operation code in a pseudocode statement must be kept all capitalized; for example READ (specifying input operation), PRINT (specifying print command), and so on.
- The ending of looping and decision-making constructs must be labelled appropriately with corresponding “END” keywords.
- The pseudocode instructions must be properly indented just like the statements are indented in a computer program.
- Convoluted programming instructions must be avoided by writing simple and clear instructions.

### 1.11.2 Advantages of Pseudocodes

- It is easy to comprehend as it uses English phrases for writing program instructions.
- Developing program code using pseudocode is easier in comparison to developing the program code from scratch.
- Developing program code using pseudocode is also easier in comparison to developing the program code from flowchart.
- The pseudocode instructions are easier to modify in comparison to a flowchart.
- The use of pseudocode works well for large program design.

Introduction to Computers, Problem Solving and Basic C 1.39

### EXAMPLE 1.13 Write the pseudocode for the problem statement given in Example 1.3.

**Solution**

```text
BEGIN
DEFINE: Integer year
DISPLAY: "Enter the year value: "
READ: year
IF: year%4=0
DISPLAY: "'year' is a leap year"
ELSE
DISPLAY: "'year' is not a leap year"
END IF
END
```

**Fig. 1.47** Pseudocode to determine whether the given year is leap or not

### EXAMPLE 1.14 Write the pseudocode for the problem statement given in Example 1.4.

**Solution**

```text
BEGIN
DEFINE: Integer num
DISPLAY: "Enter a number: "
READ: num
IF: num%2=0
DISPLAY: "'num' is an even number"
ELSE
DISPLAY: "'num' is an odd number"
END IF
END
```

**Fig. 1.48** Pseudocode to find out whether a given number is even or odd

### EXAMPLE 1.15 Write the pseudocode for the problem statement given in Example 1.5.

**Solution**

```text
BEGIN
DEFINE: String str
DEFINE: Character chk
DEFINE: Integer left, right, len
SET: chk = 't'
DISPLAY: "Enter a string: "
READ: str
COMPUTE: len = strlen(str)
SET: left = 0
SET: right = len-1
REPEAT
    IF: str(left)=str(right)
        CONTINUE
    ELSE
        SET: chk = 'f'
    END IF
    COMPUTE: left = left + 1
    COMPUTE: right = right - 1
UNTIL: left<right AND chk='t'
IF: chk='t'
    DISPLAY: "'str' is a palindrome string"
ELSE
    DISPLAY: "'str' is not a palindrome string"
END IF
END
```

**Fig. 1.49** Pseudocode to determine whether a given string is a palindrome or not

## 1.12 PROBLEM-SOLVING EXAMPLES

### EXAMPLE 1.16 Design and develop the solution for finding the roots of a quadratic equation.

**Solution**

**Algorithm**

- Step 1 - Start
- Step 2 - Accept three numbers (a, b, c) from the user for the quadratic equation ax² + bx + c
- Step 3 - Calculate root1=(-b+sqrt(b*b-4*a*c))/2*a
- Step 4 - Calculate root2=(-b-sqrt(b*b-4*a*c))/2*a
- Step 5 - Display the computed roots of the quadratic equation
- Step 6 - Stop

**Fig. 1.50** Algorithm for finding the roots of a quadratic equation

**Flowchart**

![](img/fe6da5f61b1e2c77309bbee135b45e35_52_0.png)

**Fig. 1.51** Flowchart for finding the roots of a quadratic equation

**Pseudocode**

```text
BEGIN
DEFINE: Integer a, b, c
DEFINE: Real root1, root2
DISPLAY: "Enter the values of a, b and c for the quadratic equation ax² + bx + c: "
READ: a, b, c
COMPUTE: root1=((-1)*b+sqrt(b*b-4*a*c))/2*a
COMPUTE: root2=((-1)*b-sqrt(b*b-4*a*c))/2*a
DISPLAY: "The roots of the quadratic equation are 'root1' and 'root2'"
END
```

**Program**

```c
#include<stdio.h>
#include<conio.h>
#include<math.h>

void main()
{
    int a,b,c;
    float root1,root2; /*Declaration of variables to store root values*/
    clrscr();
    printf("Enter the value a, b and c for the quadratic equation ax^2+bx+c: ");
    scanf("%d %d %d",&a, &b, &c); /*Reading values of a, b and c*/
    root1=(((-1)*b+sqrt(b*b-4*a*c))/2*a); /*Computing quadratic root1*/
    root2=(((-1)*b-sqrt(b*b-4*a*c))/2*a); /*Computing quadratic root2*/
    printf("\n\nThe roots of the quadratic equation are: %.2f %.2f",root1, root2); /*Displaying resultant roots*/
    getch();
}
```

**Output**

```text
Enter the value a, b and c for the quadratic equation ax^2+bx+c: 1
-7
12

The roots of the quadratic equation are: 4.00 3.00
```

**Fig. 1.52** Program to find the roots of a quadratic equation

### EXAMPLE 1.17 Design and develop the solution for determining whether there is profit or loss during the selling of an item.

**Solution**

**Algorithm**

- Step 1 - Start
- Step 2 - Accept the cost price and selling price of an item from the user (cp, sp)
- Step 3 - If sp>cp then goto step 4 else goto step 5
- Step 4 - Display "There is a profit of (sp-cp)" and goto Step 8
- Step 5 - If cp>sp then goto step 6 else goto step 7
- Step 6 - Display "There is a loss of (cp-sp)"
- Step 7 - Display "No profit no loss!"
- Step 8 - Stop

**Flowchart**

![](img/fe6da5f61b1e2c77309bbee135b45e35_53_0.png)

**Pseudocode**

```text
BEGIN
DEFINE: Long Integer cp, sp
DISPLAY: "Enter the cost price and selling price of an item: "
READ: cp, sp
IF: sp>cp
    DISPLAY: "There is a profit of 'sp-cp'"
ELSE
    IF: cp>sp
        DISPLAY: "There is a loss of 'cp-sp'"
    ELSE
        DISPLAY: "No profit no loss!"
    END IF
END IF
END
```

**Program**

```c
#include <stdio.h>
#include <conio.h>

void main()
{
    long cp, sp;
    clrscr();
    printf("\nEnter the cost price and selling price of an item: ");
    scanf("%ld\n%ld", &cp, &sp);  /*Reading CP and SP*/
    if(sp>cp)  /*Checking condition of profit*/
        printf("\nThere is a profit of %ld units", sp-cp);
    else if(cp>sp)  /*Checking condition of loss*/
        printf("\nThere is a loss of %ld units", cp-sp);
    else
        printf("\n\nNo Profit No Loss!");
    getch();
}
```

**Output**

```text
Enter the cost price and selling price of an item: 24
30

There is a profit of 6 units
```

**Fig. 1.53** Solution for calculating profit and loss

### EXAMPLE 1.18 Design and develop the solution for finding the area of a circle.

**Solution**

**Algorithm**

- Step 1 - Start
- Step 2 - Accept the radius of the circle from the user (radius)
- Step 3 - Calculate area of the circle using formula area = 3.14 * radius * radius
- Step 4 - Display the computed area of the circle
- Step 5 - Stop
