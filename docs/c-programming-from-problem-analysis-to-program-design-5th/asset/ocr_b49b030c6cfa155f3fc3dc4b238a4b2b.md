+   11. What is the output of the following C++ code?

```
```cpp
int *p;
int *q;
p = new int;
q = new int;
*p = 27;
*q = 35;
cout << *p << " " << *q << endl;
*q = *p;
*p = 73;
cout << *p << " " << *q << endl;
p = new int;
*p = 36;
q = p;
cout << *p << " " << *q << endl;
```
```

+   12. What is wrong with the following code?

```
```cpp
int *p;                     //Line 1
int *q;                     //Line 2

p = new int;                //Line 3
*p = 43;                    //Line 4

q = p;                      //Line 5
*q = 52;                    //Line 6

delete q;                   //Line 7

cout << *p << " " << *q << endl;    //Line 8
```
```

+   13. What is the output of the following code?

```
```cpp
int x;
int *p;
int *q;
p = new int[10];
q = p;
*p = 4;

for (int j = 0; j < 10; j++)
{
    x = *p;
    p++;
    *p = x + j;
}

for (int k = 0; k < 10; k++)
{
    cout << *q << " ";
    q++;
}
cout << endl;
```
```

+   14. What does the operator new do?

+   15. What does the operator delete do?