established between Student and Date classes. Note that, this composition is established indirectly due to inheritance (in actuality, class Person contains object of Date which is inherited by Student).

> > **NOTES**
> >
> > **Composition** should be implemented between classes whenever there exists **HAS-A** relationship in real world. For example in this case, we could say Person **HAS-A** date of birth OR Student **HAS-A** date of birth OR Professor **HAS-A** date of birth. Hence composition is also called as **HAS-A** relationship between classes.

The following is the full source code to implement the relationships between classes as shown in Figure 14.33.

```
```cpp
#include<iostream.h>
#include <Windows.h>
#include <stdio.h>
class Date
{
private:
    int dd;
    int mm;
    int yy;
public:
    void inputDate()
    {
        cout<<"Enter dd:"<<endl;
        cin>>dd;
        cout<<"Enter mm:"<<endl;
        cin>>mm;
        cout<<"Enter yyyy:"<<endl;
        cin>>yy;
    }
    void outputDate()
    {
        cout<<"dd:"<<dd<<"-"<<mm<<"-"<<yy<<endl;
    }
    void outputAge()
    {
        cout<<yy<<"years and "<<mm<<" months and "<<dd<<" days"<<endl;
    }
    static Date getCurrentDate()
    {
        SYSTEMTIME system;
        GetSystemTime(&system);
        Date today;
```
```