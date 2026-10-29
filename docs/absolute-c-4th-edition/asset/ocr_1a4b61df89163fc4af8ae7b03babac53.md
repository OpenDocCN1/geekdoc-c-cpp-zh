```
For example, the following are the first few lines from the body of the member function Hourly-Employee::printCheck (taken from Display 14.5):

```cpp
void HourlyEmployee::printCheck()
{
    setNetPay(hours * wageRate);

    cout << "\\n";
    cout << "Pay to the order of " << getName() << endl;
    cout << "The sum of " << getNetPay() << " Dollars\\n";
}
```
```

You might have wondered why we needed to use the member function setNetPay to set the value of the netPay member variable. You might be tempted to rewrite the start of the member function definition as follows:

```
```cpp
void HourlyEmployee::printCheck()
{
    netPay = hours * wageRate;
}
```
```

As the comment indicates, this will not work. The member variable netPay is a private member variable in the class Employee, and although a derived class like HourlyEmployee inherits the variable netPay, it cannot access it directly. It must use some public member function to access the member variable netPay. The correct way to accomplish the definition of printCheck in the class HourlyEmployee is the way we did it in Display 14.5 (part of which was displayed earlier).

The fact that name and netPay are inherited variables that are private in the base class also explains why we needed to use the accessor functions getName and getNetPay in the definition of HourlyEmployee::printCheck instead of simply using the variable names name and netPay. You cannot mention a private inherited member variable by name. You must instead use public accessor and mutator member functions (such as getName and setName) that were defined in the base class. (Recall that an accessor function is a function that allows you to access member variables of a class and a mutator function is one that allows you to change member variables of a class. A class accessor and mutator functions were covered in Chapter 6.)

The fact that a private member variable of a base class cannot be accessed in the definition of a member function of a derived class often seems wrong to people. After all, if you are an hourly employee and you want to change your name, nobody says, "Sorry, name is a private member variable of the class Employee." After all, if you are an hourly employee, you are also an employee. In Java, this is also true; an object of the class HourlyEmployee is also an object of the class Employee. However, the laws regarding the use of private member variables and private member functions in C++ must be as we described, or else they would be compromised. If private member variables of a class were accessible in member function definitions of a derived class, then anytime you wanted to access a private member variable, you could simply create a derived class and access it in a member function of that class, which would mean that all private member variables would be accessible to anybody who wanted to put in a little extra effort. This scenario illustrates the problem, but the big problem is unintentional errors rather than intentional

![](bbox=[0.201, 0.126, 0.854, 0.422])