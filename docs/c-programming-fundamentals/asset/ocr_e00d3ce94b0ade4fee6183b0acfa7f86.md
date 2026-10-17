```
int ecode;
void display3()
{
    cout<<"Enter exam code"<<endl;
    cin>>ecode;
}
};
class external : public student, public exam
{
    public :
    int marks;
    void display4()
    {
        cout<<"Enter your Level 1 marks"<<endl;
        cin>>marks;
    }
    void check()
    {
        if ((age>17)&&(marks>65))
        {
            cout<<"\nAllowed for Level 2 Examination\n";
        }
        else
            cout<<"Start looking for backups";
    }
};
int main()
{
    external e;
    cout<<"Enter your valid information"<<endl;
    e.display1();
    e.display2();
    e.display3();
    e.display4();
    e.check();
    return 0;
}
```

# Output:

Enter your valid information
Enter your age