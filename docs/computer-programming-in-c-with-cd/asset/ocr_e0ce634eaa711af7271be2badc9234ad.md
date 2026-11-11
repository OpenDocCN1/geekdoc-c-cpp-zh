```
}
~MorningCollege()
{
    cout<<"Morning College destructor calling"<<endl;
}
};
class EveningCollege:public College
{
public:
    EveningCollege()
    {
        cout<<"Evening College constructor calling"<<endl;
    }
    ~EveningCollege()
    {
        cout<<"Evening College destructor calling"<<endl;
    }
};
class Correspondence:public DelhiUniversity
{
public:
    Correspondence()
    {
        cout<<"Correspondence constructor calling"<<endl;
    }
    ~Correspondence()
    {
        cout<<"Correspondence destructor calling"<<endl;
    }
};
class External:public DelhiUniversity
{
public:
    External()
    {
        cout<<"External constructor calling"<<endl;
    }
    ~External()
    {
        cout<<"External destructor calling"<<endl;
    }
};
class Student:public MumbaiUniversity,public MorningCollege,public

EveningCollege,public External,public Correspondence
{
    char name[5];
    char id[10];
    int marks;
```