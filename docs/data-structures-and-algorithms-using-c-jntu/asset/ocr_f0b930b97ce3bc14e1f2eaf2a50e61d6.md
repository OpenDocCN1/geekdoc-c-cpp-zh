# Program 4.1

```
#include<iostream.h>
#include<conio.h>
#include<stdlib.h>
template<class t>
class array
{
    t a[50];
    int n,size;
    public:
    array(int m)
    {
    size=0;
    n=m;
    }
    void insert();
    void delete();
    void display();
};
template<class t>
void array<t>::insert()
{
    t ele;
    if(size==n)
    {
    cout<<"array is overflow\n";
    return;
    }
    size++;
    cout<<"enter the element\n";
    cin>>ele;
    a[size]=ele;
}
template<class t>
void array<t>::deletee()
{
    t ele;
    if(size==0)
    {
    cout<<"array is underflow\n";
    return;
    }
    ele=a[size];
    size--;
    cout<<"the deleted element is"<<ele<<"\n";
}
template<class t>
void array<t>::display()
```