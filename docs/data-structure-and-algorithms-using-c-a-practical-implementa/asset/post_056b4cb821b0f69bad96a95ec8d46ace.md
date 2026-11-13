
```cpp
void push(char no)
{
  //insert the open grouping character into stack
  top = top+1; //increase the value of top
  stack[top] = no; //store the character to stack
}
//definition of pop()
void pop(char ch)
{
  if(top == -1) //condition for underflow
  {
    cout<<"\n STACK UNDERFLOW";
    cout<<"\n INVALID EXPRESSION";
    exit(0);
  }
  //pop the character if proper closing character is found
  if(ch==')' && stack[top]=='(' || ch=='}' && stack[top]=='{' ||
     ch==']' && stack[top]=='[')
  --top; //decrease the value of top
}

int main()
{
  string str;
  int i;
  cout<<"\n ENTER THE EXPRESSION";
  cin>>str;
  for(i=0; str[i] != '\0'; i++)
  {
    if(str[i]=='(' || str[i]=='{' || str[i]=='[')
    push(str[i]);
    if(str[i]==')' || str[i]=='{' || str[i]=='}')
    pop(str[i]);
  }
  if(top == -1)
  cout<<"\n EQUATION IS CORRECT";
  else
  cout<<"\n INVALID EXPRESSION";
}
```

## OUTPUT

```
ENTER THE EXPRESSION<(a+b)*(c-d)>
EQUATION IS CORRECT
-----------------------------------
Process exited after 10.66 seconds with return value 0
Press any key to continue . . .
```

```
ENTER THE EXPRESSION a<(b-c+d)->e>
INVALID EXPRESSION
-----------------------------------
Process exited after 12.95 seconds with return value 0
Press any key to continue . . .
```

- WAP TO REVERSE A STRING BY USING STACK.

```cpp
#include<iostream>
#include<string.h>
using namespace std;
// A structure to represent a stack
class reverse
{
public:
    int top;
    int size;
    char* stk;
};
reverse* BuildStack(unsigned size)
{
    reverse* stack = new reverse();
    stack->size = size;
    stack->top = -1;
    stack->stk = new char[stack->size * sizeof(char)];
    return stack;
}
// Stack is full when top is equal to the last index
int Full(reverse* stack)
{ return stack->top == stack->size - 1; }
// Stack is empty when top is equal to -1
int Empty(reverse* stack)
{ return stack->top == -1; }
// Function to add an item to stack.
// It increases top by 1
void push(reverse* stack, char item)
{
    if (Full(stack))
        return;
    stack->stk[++stack->top] = item;
}
// Function to remove an item from stack.
// It decreases top by 1
char pop(reverse* stack)
{
    if (Empty(stack))
        return -1;
    return stack->stk[stack->top--];
}
// A stack based function to reverse a string
void Reverse(char str[])
{
    // Create a stack of capacity
    // equal to length of string
    int n = strlen(str);
    reverse* stack = BuildStack(n);

    // Push all characters of string to stack
    int i;
    for (i = 0; i < n; i++)
        push(stack, str[i]);

    // Pop all characters of string and
    // put them back to str
    for (i = 0; i < n; i++)
        str[i] = pop(stack);
}
// Driver code
int main()
{
    char str[50];
    cout<<endl<<"Enter a string";
    gets(str);
    Reverse(str);
    cout << "Reversed string is " << str;
    return 0;
}
```

## Output

```
Enter a string wel cone
Reversed string is eoc lew
---------------------------------------
Process exited after 2.132 seconds with return value 0
Press any key to continue . . .
```

In recursive methods the stack is used to store the values in each calling of the function

## EXPRESSION CONVERSIONS

In general the expressions are represented in the form of INFIX notations that is the operators are used in between the operands. But during the evaluation process the given expression is converted to POSTFIX or PREFIX according to the requirements.

- **INFIX :** The operator is used in between the operands.
  EX : A+B
- **POSTFIX :** The operator is used after the operands. It is also known as POLISH notation.
  EX : AB+
- **PREFIX :** The operator is used before the operands. It is also known as REVERSE POLISH notation.
  EX : +AB

During conversion we have to concentrate on the precedence of the operators such as

- PRECEDENCE
- FIRST : ( ), [ ], { }
- SECOND : ^, $, arrow mark
- THIRD : *, /, [Left to Right]
- FOURTH : + -, (Left to Right)

### CONVERSION OF INFIX TO POSTFIX (REVERSE POLISH) ALGORITHM

- STEP 1 : First insert an opening parenthesis at the beginning and closing parenthesis at the end of the expression.
- STEP 2 : Arrange the expression in the ARRAY.
- STEP 3 : Scan every element from the array and if operand, then store it in the POSTFIX and if operator, then PUSH it into the STACK followed by STEP-4 and STEP-5
- STEP 4 : If the scanned operator having Less or Equal precedence than the existing operator then pop out the operators from the stack till a less precedence operator or opening parenthesis is found.
- STEP 5 : If the scanned operator is a closing parenthesis then pop the operators from the STACK up to the Opening Parenthesis and omit them and popped operators will store in the POSTFIX.
- STEP 6 : Repeat step-3, step-4, step-5 till all the elements are scanned from the array.
- STEP 7 : Print the POSTFIX as the result.

### CONVERSION OF INFIX TO PREFIX (POLISH) ALGORITHM

- STEP 1 : First insert an opening parenthesis at the beginning and closing parenthesis at the end of the expression.
- STEP 2 : Arrange the expression in reverse order in the ARRAY by swapping the parenthesis (i.e. for open use close and vice versa)
- STEP 3 : Scan every element from the array and if operand, then store it in the PREFIX and if operator, then PUSH it into the STACK followed by STEP-4 and STEP-5
- STEP 4 : If the scanned operator having Less precedence than the existing operator then pop out the operators from the stack till a less precedence or Equal precedence operator or opening parenthesis is found.
- STEP 5 : If the scanned operator is a closing parenthesis then pop the operators from the STACK up to the Opening Parenthesis and omit them and popped operators will store in the PREFIX.
- STEP 6 : Repeat step-3, step-4, step-5 till all the elements are scanned from the array.
- STEP 7 : Print the PREFIX in reverse order as the result.

### EXAMPLE :

Convert A + B – (C * D – E + F ^ G) + (H + I * J) into POSTFIX by using STACK.

| ARRAY | STACK | POSTFIX |
|---|---|---|
| ( | ( | |
| A | ( | A |
| + | (+ | A |
| B | (+ | AB |
| - | (- | AB + |
| ( | (-( | AB+ |
| C | (-( | AB+C |
| * | (-(* | AB+C |
| D | (-(* | AB+CD |
| - | (-(- | AB+CD* |
| E | (-(- | AB+CD*E |
| + | (-(-+ | AB+CD*E- |
| F | (-(-+ | AB+CD*E-F |
| ^ | (-(-+^ | AB+CD*E-F |
| G | (-(-+^ | AB+CD*E-FG |
| ) | (- | AB+CD*E-FG^+ |
| + | (+ | AB+CD*E-FG^+- |
| ( | (+( | AB+CD*E-FG^+- |
| H | (+( | AB+CD*E-FG^+-H |
| + | (+(+ | AB+CD*E-FG^+-H |
| I | (+(+ | AB+CD*E-FG^+-HI |
| * | (+(+* | AB+CD*E-FG^+-HI |
| J | (+(+* | AB+CD*E-FG^+--HIJ |
| ) | (+ | AB+CD*E-FG^+--HIJ*+ |
| ) | | AB+CD*E-FG^+--HIJ*++ |

Convert A + B – (C * D – E + F ^ G) + (H + I * J) into PREFIX by using STACK.

| ARRAY | STACK | PREFIX |
|---|---|---|
| ( | ( | |
| ( | (( | |
| J | (( | J |
| * | ((* | J |
| I | ((* | JI |
| + | ((+ | JI* |
| H | ((+ | JI*H |
| ) | ( | JI*H+ |
| + | (+ | JI*H+ |
| ( | (+( | JI*H+ |
| G | (+( | JI*H+G |
| ^ | (+(^ | JI*H+G |
| F | (+(^ | JI*H+GF |
| + | (+(+ | JI*H+GF^ |
| E | (+(+ | JI*H+GF^AE |
| - | (+(+- | JI*H+GF^AE |
| D | (+(+- | JI*H+GF^AED |
| * | (+(+-* | JI*H+GF^AED |
| C | (+(+-* | JI*H+GF^EDC |
| ) | (+ | JI*H+GF^EDC*-+ |
| - | (+- | JI*H+GF^EDC*-++ |
| B | (+- | JI*H+GF^EDC*-+B |
| + | (+-++ | JI*H+GF^EDC*-+B |
| A | (+-++ | JI*H+GF^EDC*-+BA |
| ) | | JI*H+GF^EDC*-+BA++- |

FINAL RESULT i.e. PREFIX IS ++-AB+*C^DE^FG+H*IJ

## CONVERSION OF POSTFIX TO INFIX ALGORITHM

- STEP-1 : Arrange the given postfix in an array
- STEP-2 : Scan each element from the array and push it into the STACK
- STEP-3 : If an operator is found, then process it (convert it to infix) by considering the two operands and put them in a pair of parentheses.
- STEP-4 : Finally display the result.

### EXAMPLE :

Convert ABC*D-E^F/+ to INFIX

![](img/1faaa0256577c74e8a61f42967760aa8_112_0.png)
