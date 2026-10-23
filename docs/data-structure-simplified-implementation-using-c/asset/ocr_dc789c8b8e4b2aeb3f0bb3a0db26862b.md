```
// To examine whether the stack is empty.
int stacks::isEmpty ()
{
    if (top==-1)
    return 1;
    else
    return 0;
}
```

Despite of executing the push and pop operation, we are not aware of the elements that are available in the stack. To accomplish this objective, the function display () has been created. This function displays all the elements in the stack. It starts from the top and goes towards the bottom of the stack. In order to ensure that top is not shifted from the current position, a new variable with the name 'i' has been used and the value of top is assigned to this variable.

```
// Program to display the element(s) of the stack.
void stacks::display ()
{
    for (int i=top; i>=0; i--)
    cout<<stack[i]<<" ";
    cout<<endl;
}
```

On various occasions, we would need to determine the number of elements in the stack at any particular point in time. To accomplish this objective, we have created the count_elements () function.

# 5.4.1.1 Counting the number of elements

To count the number of elements in a stack, we have started from the top and moved towards the base. During this looping, variable cnt that counts the element of stack is incremented by 1. Finally, when all the elements are exhausted value of 'cnt' variable is returned to the caller function.

```
//function to count the number of element(s) in the stack;
int stacks::count_elements()
{
//initialize the t with top and cnt with 0.
int cnt=0,t=top;
// Continue till stack is not empty.
while(t>=0)
```