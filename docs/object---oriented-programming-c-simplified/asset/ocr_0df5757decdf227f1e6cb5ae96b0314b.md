```
int sup_a;
public :
    void sup_input()
    {
        cout<<"ENTER THE VALUE FOR SUP_A"<<endl;
        cin>>sup_a;
    }
    void sup_show()
    {
        cout<<"Sup_a="<<sup_a<<endl;
    }
};
class sub :public super
{
    int sub_a;
public :
    void sub_input()
    {
        sup_input();
        cout<<"Enter the value for sub_a"<<endl;
        cin>>sub_a;
    }
    void sub_show()
    {
        sup_show();
        cout<<"Sub_a="<<sub_a<<endl;
    }
};
void main()
{
    clrscr();
    sub obj;
    obj.sub_input();
    obj.sub_show();
    getch();
}
```

# OUTPUT :

ENTER THE VALUE FOR SUP_A
34
Enter the value for sub_a
45
Sup_a=34
Sub_a=45