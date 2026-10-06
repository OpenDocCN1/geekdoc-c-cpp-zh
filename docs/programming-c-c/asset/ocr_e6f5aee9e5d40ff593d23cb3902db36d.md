```
{
    cout << "This is a Vehicle" << endl;
}

// second base class
class FourWheeler {
public:
    FourWheeler()
    {
        cout << "This is a 4 wheeler Vehicle" << endl;
    }
};

// sub class derived from two base classes
class Car: public Vehicle, public FourWheeler {
};

// main function
int main()
{
    // creating object of sub class will
    // invoke the constructor of base classes
    Car obj;
    return 0;
}
```

Output:
This is a Vehicle
This is a 4-wheeler Vehicle

# Hierarchical Inheritance

In this type of inheritance, a single parent class has more than one child class. It allows accessing the code of one class in more than one derived class. Almost all computer languages supporting object oriented programming support hierarchical inheritance. The following figure depicts this kind of inheritance.