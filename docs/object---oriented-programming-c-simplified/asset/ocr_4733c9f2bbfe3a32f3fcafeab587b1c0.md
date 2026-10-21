```
first ()
{
    cout << "Hello from con first" << endl;
}
};
class second
{
public :
    second()
    {
        cout << "Hello from con of second" << endl;
    }
};
class third :second, first
{
public :
    third()
    {
        cout << "Hello from con of third" << endl;
    }
};
void main()
{
    clrscr();
    third t;
    getch();
}

OUTPUT :
Hello from con of second
Hello from con first
Hello from con of third
```

# EXPLANATION :

In multiple inheritance constructors of which base class is called determine from the fact that which class was inherited first. Here in the class third, class first and second is inherited as :

class third : second, first

So, constructor of class second will be called first and constructor of first will be called after that. Note if constructor of third class is written as :