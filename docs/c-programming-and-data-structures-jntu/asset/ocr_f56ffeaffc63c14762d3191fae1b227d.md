```
void PushOnStack(char);
int priority(char);
void ConvertToPostfix(void);
void main()
{
clrscr();
Initialize();
printf("\nEnter an infix expression: ");
gets(input);
SetExpression(input);
ConvertToPostfix();
printf("\nThe postfix expression is: ");
puts(output);
getch();
}
void Initialize(void)
{
top = -1;
strcpy(output,"");
strcpy(stack,"");
i = 0;
}
void SetExpression(char *str)
{
s = str;
l = strlen(s);
*(output + i) = '\0';
t= output;
}
/*Adding operator to the stack */
void PushOnStack ( char c)
{
if (top == MAX - 1)
printf ("\nStack is full.\n");
else
{
top++;
stack[top] = c;
}
}
/* Popping an operator from the stack */
char PopFromStack (void)
{
if (top == -1) /* Stack is empty*/
return -1;
else
{
char item = stack[top];
top--;
return item;
}
}
/* Returning the priority of the operator */
```