```
{
    int a;
    int b;
    public:
        void setvalue() {a=25; b=40; }
        friend float mean(sample s);
};
float mean(sample s)
{
    return float(s.a + s.b)/2.0;
}

int main()
{
    sample X;    // object X
    X.setvalue();
    cout << "Mean value = " << mean(X) << "\n";

    return 0;
}
```

The output of Program 5.8 would be:

Mean value = 32.5

note

> The friend function accesses the class variables a and b by using the dot operator and the object passed to it. The function call mean(X) passes the object X by value to the friend function.

Member functions of one class can be friend functions of another class. In such cases, they are defined using the scope resolution operator as shown below:

```
class X
{
    .....
    .....
    int fun1();    // member function of X
    .....
};

class Y
{
```