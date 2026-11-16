```
int num[5]={3,2,0,1,4};
disp(num,5);
}
void disp(int*x,int y)
{
int i;
for(i=0;i<y;i++)
cout<<*(x+i);
}
```

Method3: Consider the following program:

```
#include<iostream>
using namespace std;
void disp(int&,int);
int main()
{
int num[5]={3,2,0,1,4};
disp(num[0],5);
}
void disp(int&x,int y)
{
int i;
for(i=0;i<y;i++,x++)
cout<<x;
}
```

Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
```