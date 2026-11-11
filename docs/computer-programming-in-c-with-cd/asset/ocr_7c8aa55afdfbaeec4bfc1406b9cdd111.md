# ■ Passing an Object as a Function Argument-By Value

In the first method, we pass the object by value as function arguments. A copy of the object is passed to the function; any changes made to the object inside the function do not affect the object used to call the function. Listing 24 shows the addition of money in rupees and paisa using objects as function parameters (you can find this example in the ObjectsFunctionArgument_ByVal.cpp file on the CD in the code\chapter6 folder):

# ▶ Listing 24: Passing an Object by Value as a Function Parameter

```
```cpp
#include<iostream.h>

class Money
{
private:
    int rupees, paisa;
public:
    void inputData(int x, int y)
    {
        rupees=x;
        paisa=y;
    }
    void displayData()
    {
        cout<<rupees<<" Rupees and "<<paisa<<" paisa"<<endl;
    }
    void calc(Money m1, Money m2)
    {
        paisa=m1.paisa+m2.paisa;
        rupees=paisa/100;
        rupees=rupees%100;
        rupees=rupees+m1.rupees+m2.rupees;
    }
};
int main()
{
    Money m1,m2,m3;
    m1.inputData(50,67);
    m2.inputData(100,80);
    m3.calc(m1,m2);
    cout<<"Object 1 has:";
    m1.displayData();
    cout<<"Object 2 has:";
    m2.displayData();
    cout<<"Object 3 has:";
    m3.displayData();
    return 0;
}
```
```