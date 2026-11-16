```
int main()
{
    uli a=5;
    cout<<a;
    return 0;
}
```

Here, we have given an alias to unsigned long int to uli. Here, output will be 5.

Consider the following program:

```
#include<iostream>
using namespace std;
struct student
{
    char*name;
    int roll;
};
typedef struct student stu;
int main()
{
    stu s1;
    s1.roll=5;
    s1.name="Aman";
    cout<<s1.roll<<"\n";
    cout<<s1.name;
    return 0;
}
```

Output