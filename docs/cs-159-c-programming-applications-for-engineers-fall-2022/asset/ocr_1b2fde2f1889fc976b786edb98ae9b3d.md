# A Function with Arguments that Returns a Value

```
```c
#include<stdio.h>

//FUNCTION DECLARATIONS
void welcome (void);
int getInput (void);
int calcRemainder (int, int);
int calcQuotient (int, int);

int main (void)
{
    //LOCAL VARIABLE DECLARATIONS
    int operand1; //FIRST OPERAND ENTERED BY USER
    int operand2; //SECOND OPERAND ENTERED BY USER
    int remainder; //HOLDS THE RESULT OF THE REMAINDER
    int quotient; //HOLDS THE RESULT OF INT DIVISION

    //EXECUTABLE STATEMENTS
    welcome ();

    operand1 = getInput (); //THE ASSIGNMENT OPERATOR AWAITS THE
    operand2 = getInput (); //VALUE RETURNED FROM operand1

    remainder = calcRemainder(operand1, operand2);
    quotient = calcQuotient(operand1, operand2);

    return(0);
}
```
```