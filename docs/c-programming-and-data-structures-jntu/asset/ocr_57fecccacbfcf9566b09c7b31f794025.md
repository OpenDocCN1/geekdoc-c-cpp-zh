```
{
 top = -1;
 strcpy(output,"");
 strcpy(stack,"");
 i = 0;
}
void SetExpression(char *str)
{
 s = str;
 i = strlen(s);
 *(output + i) = '\0';
 t= output;
}
/*Adding operator to the stack */
void PushOnStack(char c)
{
 if (top == MAX - 1)
 printf("\nStack is full.\n");
 else
 {
 top++;
 stack[top] = c;
 }
}
/*Popping an operator from the stack*/
char PopFromStack(void)
{
 if (top == -1)
 return -1;
 else
 {
 char item = stack[top];
 top--;
 return item;
 }
}
/* Returning the priority of the operator */
int priority(char c)
{
 if (c=='^') return 3;
 if (c=='*' || c=='/' || c=='%')
 return 2;
 else if (c=='+' || c=='-') return 1;
 else return 0;
}

/* Converting the Infix expression to Prefix*/
void ConvertToPrefix(void)
{
 char opr;
 while (*s)
 {
 if (*s=='=' || *s=='^')
 {
 s++;

```