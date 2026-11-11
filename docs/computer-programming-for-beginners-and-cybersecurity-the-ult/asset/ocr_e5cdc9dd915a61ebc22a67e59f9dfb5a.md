> >New value: 3

> >New value: 5

> >New value: 8

> >New value: 13

There're a few things to note, the lack of iteration loops, recursion in its essence causes looping. The second thing to note if the if statement labelled 'stopping condition,' if recursive set-ups don't have conditions that stop them looping they will loop forever, so this is a crucial element for using recursion effectively.

We touched on recursion in the basic section of the tutorial, and again it's the definition of a function's tasks with definition to itself. As promised, there are a few more examples of recursion explained below:

```
```c
int factorial(int x)
{
int r;
//Stopping condition
if (x == 1)
{
//Has a conclusion so looping stop
return 1;
}
else
{
//Recursive definition
return r = x * factorial(x - 1);
```
```