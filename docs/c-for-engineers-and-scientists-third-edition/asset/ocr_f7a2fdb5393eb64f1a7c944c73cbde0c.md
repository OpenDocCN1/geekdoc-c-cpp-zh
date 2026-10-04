```
// class implementation for One
One::One(double val) // constructor
{
    a = val;
}
```

```
double One::f1(double number) // a member function
{
    return(num/2);
}
```

```
double One::f2(double number) // another member function
{
    return(pow(f1(num),2)); // square the result of f1
}
```

```
// class declaration section for the derived class
class Two : public One

public:
    virtual double f1(double); // this overrides class One's f1()
}
```

```
// class implementation section for Two
double Two::f1(double number)
{
    return(num/3);
}
```

```
int main() {
    One object_1; // object_1 is an object of the base class
Two object_2; // object_2 is an object of the derived class

    // call f2() using a base class object call
    cout << "The computed value using a base class object call is "
         << object_1.f2(12) << endl;

    // call f2() using a derived class object call
    cout << "The computed value using a derived class object call is "
         << object_2.f2(12) << endl;

    return 0;
}
```