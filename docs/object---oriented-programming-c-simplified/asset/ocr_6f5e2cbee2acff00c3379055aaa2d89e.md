Its general syntax is :

```
```cpp
if(condition)
{
    Statements;
    Statements;
    ............;
}
else
{
    Statements;
    Statements;
    ............;
}
```
```

If the condition within if true all the statements within the block following if are executed else they are skipped and else part get executed.

```
```cpp
/*PROG 3.30 CHECKING THE NUMBER IS EVEN OR ODD USING IF–ELSE STATEMENT*/
#include<iostream.h>
void main( )
{
    int a;
    cout << “Enter any integer number \n ”;
    cin >> a;
    if(a%2 == 0)
        cout << “number is even\n”;
    else
        cout << “number is odd\n”;
}

OUTPUT :
(First run)
Enter any integer number
40
number is even
(Second Run)
Enter any integer number
17
number is odd
```
```