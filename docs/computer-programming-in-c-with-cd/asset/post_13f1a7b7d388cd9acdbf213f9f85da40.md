
Output:

```text
Object 1 has:50 Rupees and 67 paisa
Object 2 has:100 Rupees and 80 paisa
Object 3 has:151 Rupees and 147 paisa
```

In Listing 24, three objects, m1, m2, and m3, of the Money class are created in the main() function. The objects, m1 and m2, are calling the inputData() function to take data values, while the m3 object is calling the calc() function to calculate money. Each object is displaying the values stored in them by using the displayData() function. The inputData() function is having two arguments in which numerical values are passed for money calculation. The calc() function is taking the m1 and m2 objects as its arguments. In the function definition of the calc() function, the variables of the m3 object are used, but the variables of m1 and m2 objects are called by using the dot (.) operator, such as m1.rupees and m1.paisa. Finally, each object (m1, m2, and m3) is showing the money value that is stored in these objects.

### Passing an Object as a Function Argument-By Reference

An object can be passed by reference (address of the object) as a function argument. When the address of an object is passed as function argument, the function works directly on the actual object. This method is more efficient as it requires passing only the address of the object and not the entire object. Listing 25 shows how an object reference is passed as a function parameter (you can find this example in the ObjectsFunctionArguments_ByRef.cpp file on the CD in the code\chapter6 folder):

**Listing 25: Passing an Object Reference as a Function Parameter**

```cpp
#include<iostream.h>

class MoneyTransfer
{
private:
    int acc_no;
    float bal;
public:
    void inputData()
    {
        cout<<"Enter account number:"<<endl;
        cin>>acc_no;
        cout<<"Enter the balance:"<<endl;
        cin>>bal;
    }
    void setData(int acno)
    {
        acc_no=acno;
        bal=0;
    }
    void setData(int x, float y)
    {
        acc_no=x;
        bal=y;
    }
    void displayData()
    {
        cout<<"Account Number: "<<acc_no<<endl;
        cout<<"Balance is : "<<bal<<endl;
    }
    void calc(MoneyTransfer &m, float x);
};
void MoneyTransfer::calc(MoneyTransfer &m, float x)
{
    bal=bal-x; //money deduction from source
    m.bal=m.bal+x; //add money to destination
}

int main()
{
    MoneyTransfer m1,m2,m3;
    int money_trans;
    m1.inputData();
    m2.setData(50);
    m3.setData(80,456.89F);
    cout<<"Account Information"<<endl;
    m1.displayData();
    m2.displayData();
    m3.displayData();
    cout<<"Enter money for transferring from Account3 to Account1:";
    cin>>money_trans;
    m3.calc(m1,money_trans);
    cout<<"Updated Account Information"<<endl;
    m1.displayData();
    m2.displayData();
    m3.displayData();
    return 0;
}
```

Output:

```text
Enter account number:
10001
Enter the balance:
2000
Account Information
Account Number: 10001
Balance is : 2000
Account Number: 50
Balance is : 0
Account Number: 80
Balance is : 456.89
Enter money for transferring from Account3 to Account1:100
Updated Account Information
Account Number: 10001
Balance is : 2100
Account Number: 50
Balance is : 0
Account Number: 80
Balance is : 356.89
```

In Listing 25, m1, m2, and m3 are three objects of the MoneyTransfer class. The MoneyTransfer class has the calc(MoneyTransfer &m, float x) function that takes the reference of the m object of the MoneyTransfer class as one of its parameters. The following code snippet shows definition of the calc(MoneyTransfer &m, float x) function:

```cpp
void MoneyTransfer::calc(MoneyTransfer &m, float x)
{
    bal=bal-x;          //money deduction from source
    m.bal=m.bal+x;      // add money to destination
}
```

In the preceding code snippet, the variables of the MoneyTransfer class are accessed directly, while the variables of the m object of the MoneyTransfer class are accessed by using the object and the class member access operator. The following code snippet shows that the m1 object is passed as an argument of the calc() function:

```cpp
m3.calc(m1,money_trans);
```

In the preceding code snippet, the calc() function, which takes the m1 object as an argument, is invoked with the m3 object. Note that when the calc() function is invoked with the m3 object, the data members of the m3 object are accessed without using the class member access operator; whereas, the data members of the m1 object are accessed by using the object and the class member access operator.

An object can also be passed as an argument to a non-member function. However, such non-member functions have limited access only. These functions can access the public members of a class, not private members, by passing objects as function arguments.

Listing 26 shows how non-member function accepts object address as parameters (you can find this example in the NonMemberFunctions_ObjectAddress.cpp file on the CD in the code\chapter6 folder):

### 6.9 Returning Objects from Functions

A function can also return an object, as well as a variable. This means that a class can be declared as a return type of the function. The functions that return objects can be one of the following kinds:

- Non-member functions
- Member functions of a class

#### Returning Objects from non-member Functions

A function definition that is not a part of any class declaration is called a non-member function. In C++, it is possible for a non-member function to have a class as its return type. It means that a non-member function can return an object of a class. Listing 27 shows an object returning a non-member function (you can find this example in the NonMemberFunction_ReturnObject.cpp file on the CD in the code\chapter6 folder):

**Listing 27: Creating a Non-Member Function Returning an Object**

```cpp
#include<iostream.h>

class InterestCalculator
{
private:
    int principle, rate, time, SI;
public:
    void inputData(int x, int y, int z)
    {
        cout<<"\tSimple Interest Calculator"<<endl;
        principle=x;
        rate=y;
        time=z;
        cout<<"Principle:"<<principle<<endl;
        cout<<"Rate:"<<rate<<endl;
        cout<<"Time:"<<time<<endl;
    }
    void displayData()
    {
        SI=principle*rate*time/100;
        cout<<"Interest is:"<<SI<<endl;
    }
};
InterestCalculator MyFunc()
{
    InterestCalculator o1;
    o1.inputData(1000,10,1);
    return o1;
}
int main()
{
    InterestCalculator o2;
    o2.inputData(10000,20,1);
    o2=MyFunc();
    o2.displayData();
    return 0;
}
```

Output:

```text
                    Simple Interest Calculator
Principle:10000
Rate:20
Time:1
                    Simple Interest Calculator
Principle:1000
Rate:10
Time:1
Interest is:100
```

In Listing 27, InterestCalculator is a class that has the inputData() and displayData() member functions. The MyFunc() function does not belong to the InterestCalculator class, but has the return type as InterestCalculator. This means that the MyFunc() function returns the object of the InterestCalculator class.

After learning how to code a non-member function that returns an instance (or object) of a class, let’s learn how to define a member function of class as an object returning function.

#### Returning Objects from Member Functions

As you know, a function defined within a class declaration is called a member function of that class. A member function can also return an object of a class. It means that a member function can also have a class as its return type. Listing 28 shows an object returning member function (you can find the example in the MemberFunction_ReturnObject.cpp file on the CD in the code\chapter6 folder):

**Listing 28: Creating a Member Function Returning an Object**

```cpp
#include<iostream.h>

class InterestCalculator
{
private:
    int principle, rate, time, SI;
public:
    void inputData(int x, int y, int z)
    {
        cout << "\tSimple Interest Calculator" << endl;
        principle=x;
        rate=y;
        time=z;
        cout << "Principle:" << principle << endl;
        cout << "Rate:" << rate << endl;
        cout << "Time:" << time << endl;
    }
    void displayData(InterestCalculator cal)
    {
        SI=cal.principle*cal.rate*cal.time/100;
        cout << "Interest is:" << SI << endl;
    }
    InterestCalculator MyFunc(InterestCalculator ic)
    {
        InterestCalculator o1;
        o1.principle=principle+ic.principle;
        o1.rate=ic.rate;
        o1.time=ic.time;
        return o1;
    }
};
int main()
{
    InterestCalculator ic1,ic2,ic3;
    ic1.inputData(1000,10,1);
    ic2.inputData(2000,30,5);
    ic3=ic1.MyFunc(ic2);
    cout << "Object 1 calling" << endl;
    ic1.displayData(ic1);
    cout << "Object 2 calling" << endl;
    ic2.displayData(ic2);
    cout << "Object 3 calling" << endl;
    ic3.displayData(ic3);
    return 0;
}
```

Output:

```text
             Simple Interest Calculator
Principle:1000
Rate:10
Time:1

             Simple Interest Calculator
Principle:2000
Rate:30
Time:5
Object 1 calling
```
