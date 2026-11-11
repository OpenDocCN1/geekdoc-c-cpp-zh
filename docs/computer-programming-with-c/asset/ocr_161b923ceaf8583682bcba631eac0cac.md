![](bbox=[0.219, 0.109, 0.804, 0.335])

> **NOTES**
> 
> **UML** stands for unified modelling language. It is a language which gives set of notations to represent relationships between classes. Scope of UML is not just modelling of classes; it has many modelling notations which cover the complete software development lifecycle right from requirement gathering to maintenance of the developed system. Figures drawn with UML notations simplify the studies required in **object oriented analysis and design** paradigms. The detailed study of UML is out of scope of this text book but we have mentioned about it here because we have used one of the UML notations in Figure 11.48.

The following is the full source code, which shows the creation of composition between classes Student and MarkSheet:

```
```cpp
#include<iostream.h>
class MarkSheet
{
    private:
        int m1,m2,m3;
    public:
    void inputMarks()
    {
    cout<<"Enter Marks m1,m2 and m3"<<endl;
    cin>>m1>>m2>>m3;
    }
    void printMarks()
    {
    cout<<"......:Marks obtained in individual subjects
are:::"<<endl;
    cout<<"m1="<<m1<<"m2="<<m2<<"m3="<<m3<<endl;
    }
    friend class Student;
};
```
```