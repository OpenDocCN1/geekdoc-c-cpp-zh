```
```cpp
}
~Vehicle()
{
    cout<<"Destructor of Vehicle class"<<endl;
}
};
class Maruti:public Vehicle
{
    public:
    Maruti()
    {
        cout<<"Constructor of Maruti class"<<endl;
    }
    ~Maruti()
    {
        cout<<"Destructor of Maruti class"<<endl;
    }
};
class Car:public Maruti
{
    public:
    Car()
    {
        cout<<"Constructor of Car class"<<endl;
    }
    ~Car()
    {
        cout<<"Destructor of Car class"<<endl;
    }
};
int main()
{
    Car zen;
    cout<<"Main program is here"<<endl;
    return 0;
}
```
```

# Output:

Constructor of Vehicle class  
Constructor of Maruti class  
Constructor of Car class  
Main program is here  
Destructor of Car class  
Destructor of Maruti class  
Destructor of Vehicle class