# 12 is not prime

Here, since we have nothing to return, so we have used void as return type.

Consider the following program:

```
#include<iostream>
using namespace std;
void welcome();
void bye(void);
int main()
{
    welcome();
    bye();
}
void welcome()
{
    cout<<"Welcome\n";
}
void bye()
{
    cout<<"Bye";
}
```

Output:

Welcome

Bye