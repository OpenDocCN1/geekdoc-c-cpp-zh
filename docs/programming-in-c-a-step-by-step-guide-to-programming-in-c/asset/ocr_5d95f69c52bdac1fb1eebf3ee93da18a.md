```
```c
}
else
{
printf("The stack is full can not push a value\\n");
exit(0);
}
}

void pop(int stack[], int *top, int *value)
{
if(*top >= 0)
{
*value = stack[*top];
*top = *top - 1;
}
else
{
printf("The stack is empty can not pop a value\\n");
exit(0);
}
}

void main()
{
int stack[MAX];
```
```