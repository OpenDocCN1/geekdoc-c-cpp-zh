```
int m;
public:

opOverload()
{
}
void values()
{
    cout<<"\nEnter any number\n";
    cin>>m;
}

void operator ++()
{
    m++;
}
void display()
{
    cout<<"\nFirst Number now is "<<m<<endl;
}
};

int main()
{
    opOverload obj1;
    obj1.values();
    obj1++;
    obj1.display();
    return 0;
}
```

# Output:

Entry any number
33
First number now is 34

# Code Debriefing

+   In this code, we have created a class with a few methods.

+   The values() method is used to accept input for data members from the user.