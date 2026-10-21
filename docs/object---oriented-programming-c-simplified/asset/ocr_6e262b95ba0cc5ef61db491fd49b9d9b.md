# Object-Oriented Programming C++ Simplified

```
/*PROG 3.49 FOR LOOP SYNTAX-4 VER*/
#include <iostream.h>
void main()
{
int t;
for(t=1;t<=10;)
cout << " " << t++;
}

OUTPUT :

1 2 3 4 5 6 7 8 9 10
```

![](bbox=[0.25, 0.38, 0.75, 0.48])

EXPLANATION : Here the mistake done in the above program has been removed. After printing the value of t it will be incremented (due to post increment). for loop works fine and prints 1 to 10.

```
/*PROG 3.50 FOR LOOP SYNTAX-3 VER 1*/
#include <iostream.h>
void main()
{
int t;
t = 1;
for(t<=10;)
cout << "t: " << t++ << endl;
}

OUTPUT :

t: 1 t: 2 t: 3 t: 4 t: 5 t: 6 t: 7 t: 8 t: 9 t: 10
```

![](bbox=[0.25, 0.88, 0.75, 0.95])

EXPLANATION : In this program we have left both unitization and increment/decrement part, still semicolon is necessary on both sides. The general syntax is :