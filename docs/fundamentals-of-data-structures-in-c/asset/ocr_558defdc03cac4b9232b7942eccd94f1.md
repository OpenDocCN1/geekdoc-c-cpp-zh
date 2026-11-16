```
```c
char ip[MAX][2] = {
    {'(', MAX}, {')', 0 }, {'\0', 0}, {'+', 1},
    {'-', 1}, {'*', 2}, {'/', 2}, {'%', 2},
    {'\0', 3}
};
```
```

```
```c
char sp[MAX][2] = {
    {'(', 0}, {')', -1}, {'\0', 0}, {'+', 1},
    {'-', 1}, {'*', 2}, {'/', 2}, {'%', 2},
    {'\0', 3}
};
```
```

```
```c
void main()
{
    char inStr[20], postStr[20];
    printf("Enter the infix expression : ");
    scanf("%s", inStr);
    inToPost(inStr, postStr);
    printf("The postfix expression is : %s", postStr);
}
```
```

```
```c
int push(char value)
{
    extern stack *topStk;
    stack *newptr;
    newptr = getNode();
    if(newptr == NULL)
    return -1;
    newptr -> data = value;
    newptr -> next = topStk;
    topStk = newptr;
    return 0;
}
```
```

```
```c
int pop(char *value)
{
    extern stack *topStk;
    stack *temp;
    if(topStk == NULL)
    return -1;
    temp = topStk;
    topStk = topStk -> next;
    *value = temp -> data;
    releaseNode(temp);
    return 0;
}
```
```