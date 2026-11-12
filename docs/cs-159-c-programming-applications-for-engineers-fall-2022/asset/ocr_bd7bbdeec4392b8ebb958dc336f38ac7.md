# A Function with no Parameters that Returns a Value

+   • Input functions are a good example of the category of functions which accept no data into the function but are able to generate and return a single value.

```
#include<stdio.h>
//FUNCTION DECLARATIONS
void welcome(void);
int getInput(void);
int main(void)
{
//LOCAL VARIABLE DECLARATIONS
int operandi; //FIRST OPERAND ENTERED BY USER
int operand2; //SECOND OPERAND ENTERED BY USER
//EXECUTABLE STATEMENTS
welcome();
operand1 = getInput(); //THE ASSIGNMENT OPERATOR AWAITS THE
operand2 = getInput(); //VALUE RETURNED FROM operandInput
return(0);
}
```

Why does the order in which the functions are called matter? Why not add the two executable statements to be first?

Why would you consider the addition of a print statement to display the values of the two integers after the two function calls?

What would happen if you printed these two integers before the two function calls?