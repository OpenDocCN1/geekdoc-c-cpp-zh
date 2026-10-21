```
int num;
public :
    void input(int x)
    {
        num =x;
    }
    int getnum()
    {
        return num;
    }
    long int getrev();
};

long int Revnum ::getrev()
{
    int save = num, r, rev = 0;
    while (save!=0)
    {
        r = save % 10;
        rev = rev*10 + r;
        save = save/10;
    }
    return rev;
}

void main()
{
    Revnum obj;
    int x;
    clrscr();
    cout<<"ENTER THE NUMBER";
    endl(cout);
    cin>>x;
    obj.input(x);
    cout<<"reverse of "<<obj.getnum()
    <<" is "<<obj.getrev()<<endl;
    getch();
}
```