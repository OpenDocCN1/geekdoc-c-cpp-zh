```
~~~cpp
cout<<endl;
cout<<"Enter salary : ";
cin>>salary;
}
void displayRegular()
{
    cout<<"Experience : "<<experience<<endl;
    cout<<"Salary : "<<salary<<endl;
}
};
class Casual: public SalesPerson
{
    public:
    int duration;

    void getCasual()
    {
        cout<<"Enter duration : ";
        cin>>duration;
    }
    void displayCasual()
    {
        cout<<"Duration : "<<duration<<endl;
    }
};
void main()
{
    Typist t;
    SalesPerson sp;
    Officer o;
    Regular r;
    Casual c;
    int ch;
    char choice;
    do
    {
        cout<<"Employee Details"<<endl;
        cout<<"1 : Typist"<<endl;
        cout<<"2 : Sales Person (Regular)"<<endl;
        cout<<"3 : Sales Person (Casual)"<<endl;
        cout<<"4 : Officer"<<endl;
        cin>>ch;
        switch(ch)
        {

            case 1:
                t.getStaff();
                t.getTypist();
                t.displayStaff();
                t.displayTypist();
~~~
```