This is done as :

```
void push(int item)
{
    if(top == 9)
    {
        cout << "STACK IS FULL" << endl;
        exit(0);
    }
```

If top= =9, stack is full and we terminate the program.

When an item is popped we take the value at st[top] and decrement the top by 1 as return st[top-]. Before popping an item we check stack is empty or not. This is done as follows :

```
if(top == -1)
{
    cout << "STACK IS EMPTY" << endl;
    exit(0);
}
```

If top= = -1, stack is empty and we terminate the program.

```
/*PROG 7.10 QUEUE SIMULATION USING ARRAY AND CLASS */

#include <iostream.h>
#include <conio.h>
#include <stdlib.h>
#define S 5

class queue
{
    int front;
    int rear;
    int que[S];

public :

    queue()
    {
        front = rear = -1;
    }

    void insert(int item)
    {
```