Q2. What will be the output of the following program?

```
```cpp
#include <iostream.h>

int main()
{
  int a=25,b;
  int *x,*y;
  x=&a;
  y=&b;
  b=50;
  cout<<"Value of a: "<<x<<"\n";
  cout<<"Value of b: "<<y<<"\n";
  return 0;
}
```
```

Ans. Output of the preceding program is as follows:

```
```text
value of a: 25
value of b: 50
```
```

Q3. What will be the output of the following program?

```
```cpp
#include <iostream.h>

void swap (int *num1, int *num2)
{
  int temp;
  temp = *num1;
  *num1=*num2;
  *num2=temp;
}
int main()
{
  int a=25,b=50;
  int *x,*y;
  x=&a;
  y=&b;
  swap (x,y);
  cout<<"Value of a: "<<x<<"\n";
  cout<<"Value of b: "<<y<<"\n";
  return 0;
}
```
```

Ans. Output of the preceding program is as follows:

```
```text
value of a: 50
value of b: 25
```
```