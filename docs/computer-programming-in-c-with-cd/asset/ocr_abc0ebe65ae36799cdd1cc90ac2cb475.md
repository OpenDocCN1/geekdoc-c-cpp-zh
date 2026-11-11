```
```cpp
int variable1, variable2, variable3;
public:
    void initialize();
    void greaterNum();
    void displayNum();
};
void GreatestNumber::initialize()
{
    variable1=10;
    variable2=20;
}
void GreatestNumber::greaterNum()
{
    if(variable1>=variable2)
        variable3=variable1;
    else
        variable3=variable2;
}
void GreatestNumber::displayNum()
{
    cout<<"The greatest number is:"<<variable3<<endl;
}

int main()
{
    GreatestNumber gnObject1;
    gnObject1.initialize();
    gnObject1.greaterNum();
    gnObject1.displayNum();
    return 0;
}
```
```

# Output:

The greatest number is:20

In Listing 9, the gnObject1 object of the GreatestNumber class has to call a member function, initialize (), to initialize the data members, variable1 and variable2. The only drawback of this approach is that if the user forgets to invoke the initialization function, the program operates on an object that has member variables with meaningless values (junk characters). It is because, when a variable is declared within a class, it just stores some junk characters (meaningless values) within it.

C++ offers a solution to this problem. While designing a class, you can include a special member function within the class that is executed whenever an object of the class is created. Such functions are called constructors. Constructors are the member functions of a class and are invoked when an instance of the class, to which they belong, is created.