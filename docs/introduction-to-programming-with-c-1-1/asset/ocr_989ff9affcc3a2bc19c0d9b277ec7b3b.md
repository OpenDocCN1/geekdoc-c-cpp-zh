+   2. Set item=stack[top]
+   3. Set top=top-1
+   4. Print "Item deleted"
+   5. Print "Stack under flow"

# Example

```
void pop()
{
int item;
if(top==-0)
{
printf("\\nStack is empty: ");
}
else
{
s.item=s.stack[top];
top=top-1;
printf("deleted data is: %d",s.item);
}
}
```

[https://www.sitesbay.com/data-structure/c-stack-pop-operation](https://www.sitesbay.com/data-structure/c-stack-pop-operation)

# Example of Stack in C

Program of stack is very simple when you insert any item in stack top will be increased by 1 and when you pop any item from stack top will be decreased by 1. Both insertion and deletion operation in stack perform from top of stack.

# Example

```
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>

#define size 5
```