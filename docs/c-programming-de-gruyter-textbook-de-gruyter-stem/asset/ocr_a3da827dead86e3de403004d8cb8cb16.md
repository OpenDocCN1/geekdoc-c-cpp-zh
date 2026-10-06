# 192 — 5 Data Sharing and Protecting

```
void employee::SetAccumPay(float pa)
{ accumPay=pa; } //set monthly pay
```

```
int employee::GetindividualEmpNo()
{ return individualEmpNo; } //get member number
```

```
int employee::Getgrade()
{ return grade; } //get grade
```

```
float employee::GetAccumPay()
{ return accumPay; } //set monthly pay
```

```
//5_11.cpp
#include<iostream>
#include"employee.h"
using namespace std;
int main()
{
    employee m1;
    employee t1;
    employee sm1;
    employee s1;
    cout<<"Please enter an employee's monthly pay":
    float pa;
    cin>>pa;
    m1.promote(3); //promote m1 by 3 levels
    m1. SetAccumPay(pa); //set monthly pay of m1

    cout<<"Please enter an employee's monthly pay":"\n    cin>>pa;
    t1.promote(2); //promote t1 by 2 levels
    t1. SetAccumPay(pa); //set monthly pay of t1

    cout<<"Please enter an employee's monthly pay":"\n    cin>>pa;
    sm1.promote(2); //promote s1 by 2 levels
    sm1. SetAccumPay(pa); //set monthly pay of sm1

    cout<<"Please enter an employee's monthly pay":"\n    cin >>pa;
    s1. SetAccumPay(pa); //set monthly pay of s1
}
```