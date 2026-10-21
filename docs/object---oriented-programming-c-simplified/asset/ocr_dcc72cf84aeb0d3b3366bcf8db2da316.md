```
{
    cout<<"Hello from show of third class"<<endl;
}
};
void main()
{
    clrscr();
    first *fptr;
    first f;
    second s, *sptr;
    third t;
    fptr = &f;
    fptr->show();
    fptr = &s;
    fptr->show();
    sptr = &s;
    sptr->show();
    sptr = &t;
    sptr->show();
    getch();
}
```

# OUTPUT :

Hello from show of first class
Hello from show of first class
Hello from show of second class
Hello from show of third class

# EXPLANATION :

The function show is not virtual in the class first and first is the base class for class second. So the statement
fptr = &s;
fptr->show();
Executes show of class first will be called. The class second is the base class for class third. In class second show is virtual and this show in class third is overridden. In the statement
sptr = &s;
sptr->show();
sptr contains the address of second class object so function show of class second is called. In the following statements as :
sptr = &t;
sptr->show();
sptr contains the address of object of class third. As show is virtual in the class second so function of class third will be called.