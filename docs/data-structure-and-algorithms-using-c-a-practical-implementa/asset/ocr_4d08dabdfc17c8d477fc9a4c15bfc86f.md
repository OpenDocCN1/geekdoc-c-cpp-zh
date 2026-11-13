```
```c
// Stack is empty when top is equal to -1
int Empty(reverse* stack)
{ return stack->top == -1; }
```
```

```
```c
// Function to add an item to stack.
// It increases top by 1
void push(reverse* stack, char item)
{
    if (Full(stack))
        return;
    stack->stk[++stack->top] = item;
}
```
```

```
```c
// Function to remove an item from stack.
// It decreases top by 1
char pop(reverse* stack)
{
    if (Empty(stack))
        return -1;
    return stack->stk[stack->top--];
}
```
```

```
```c
// A stack based function to reverse a string
void Reverse(char str[])
{
    // Create a stack of capacity
    // equal to length of string
    int n = strlen(str) ;
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
```
```

```
```c
// Driver code
int main()
{
    char str[50];
    cout<<endl<<"Enter a string";
    gets(str);
```
```