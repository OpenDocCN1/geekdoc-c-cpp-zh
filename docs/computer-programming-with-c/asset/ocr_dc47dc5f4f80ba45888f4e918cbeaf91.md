```
#include<iostream.h>
class Person
{
protected:
    int id;
    char name[100];
public:
    void input()
    {
        cin>>id>>name;
    }
    void output()
    {
        cout<<id<<" "<<name<<endl;
    }
}; class Student: public Person
{
private:
int marks;
public:
    void input()
    {
        cin>>id>>name>>marks;
    }
    void output()
    {
        cout<<id<<" "<<name<<"  "<<marks<<endl;
    }
};
void main()
{
Person p1;
Student s1;
Person *p;
p=&p1;
cout<<"Enter id and name of Person "<<endl;
p->input();
cout<<"Person details are: "<<endl;
p->output ();
p=&s1;
cout<<"Enter id, name and marks of Student"<<endl;
((Student*)p)->input();
```