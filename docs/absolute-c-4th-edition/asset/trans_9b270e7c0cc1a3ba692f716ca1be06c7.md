

## Display 14.6 Implementation for the Derived Class SalariedEmployee (part 2 of 2)

```
42      cout << "Salaried Employee. Regular Pay: "
43      cout << salary << endl;
44      cout << "--------------------------------------------------\n";
45    }
46 }//SavitchEmployees
```

## CONSTRUCTORS IN DERIVED CLASSES

A constructor in a base class is not inherited in the derived class, but you can invoke a constructor of the base class within the definition of a derived class constructor, which is all you need or normally want. A constructor for a derived class uses a constructor from the base class in a special way: A constructor for the base class initializes all the data inherited from the base class. Thus, a constructor for a derived class begins with an invocation of a constructor for the base class. The special syntax for invoking the base class constructor is illustrated in the constructor definitions for the class HourlyEmployee given in Display 14.5. In what follows we have reproduced (with minor changes in the line breaks to make it fit the text column) one of the constructor definitions for the class HourlyEmployee taken from that display:

```
HourlyEmployee::HourlyEmployee(string theName,
    string theNumber, double theWageRate, double theHours)
  : Employee(theName, theNumber),
    wageRate(theWageRate), hours(theHours)
{
    //deliberately empty
}
```

The portion after the colon is the initialization section of the constructor definition for the constructor HourlyEmployee::HourlyEmployee. The part Employee(theName, theNumber) is an invocation of the two-argument constructor for the base class Employee. Note that the syntax for invoking the base class constructor is analogous to the syntax used to set member variables: The entry wageRate(theWageRate) sets the value of the member variable wageRate to theWageRate; the entry Employee(theName, theNumber) invokes the base class constructor Employee with the arguments theName and theNumber. Since all the work is done in the initialization section, the body of the constructor definition is empty.

Below we reproduce the other constructor for the class HourlyEmployee from Display 14.5:

```
HourlyEmployee::HourlyEmployee() : Employee(), wageRate(0),
    hours(0)
{
    //deliberately empty
}
```

## AN OBJECT OF A DERIVED CLASS HAS MORE THAN ONE TYPE

In everyday experience an hourly employee is an employee. In C++ the same sort of thing holds. Since HourlyEmployee is a derived class of the class Employee, every object of the class HourlyEmployee can be used anyplace an object of the class Employee can be used. In particular, you can use an argument of type HourlyEmployee when a function requires an argument of type Employee. You can assign an object of the class HourlyEmployee to a variable of type Employee. (But be warned: You cannot assign a plain old Employee object to a variable of type HourlyEmployee. After all, an Employee is not necessarily an HourlyEmployee.) Of course, the same remarks apply to any base class and its derived class. You can use an object of a derived class anyplace that an object of its base class is allowed.

More generally, an object of a class type can be used anyplace that an object of any of its ancestor classes can be used. If class Child is derived from class Ancestor and class Grandchild is derived from class Child, then an object of class Grandchild can be used anyplace an object of class Child can be used, and the object of class Grandchild can also be used anyplace that an object of class Ancestor can be used.

In this constructor definition the default (zero-argument) version of the base class constructor is called to initialize the inherited member variables. You should always include an invocation of one of the base class constructors in the initialization section of a derived class constructor.

If a constructor definition for a derived class does not include an invocation of a constructor for the base class, then the default (zero-argument) version of the base class constructor will be invoked automatically. So, the following definition of the default constructor for the class HourlyEmployee (with Employee() omitted) is equivalent to the version we just discussed:

```
HourlyEmployee::HourlyEmployee( ) : wageRate(0), hours(0)
{
    //deliberately empty
}
```

However, we prefer to always explicitly include a call to a base class constructor, even if it would be invoked automatically.

A derived class object has all the member variables of the base class. When a derived class constructor is called, these member variables need to be allocated memory and should be initialized. This allocation of memory for the inherited member variables must be done by a constructor for the base class, and the base class constructor is the most convenient place to initialize these inherited member variables. That is why you should always include a call to one of the base class constructors when you define a constructor for a derived class. If you do not include a call to a base class constructor (in the initialization section of the definition of a derived class constructor), then the

default (zero-argument) constructor of the base class is called automatically. (If there is no default constructor for the base class, an error occurs.)

The call to the base class constructor is the first action taken by a derived class constructor. Thus, if class B is derived from class A and class C is derived from class B, then when an object of class C is created, first a constructor for class A is called, then a constructor for B is called, and finally the remaining actions of the class C constructor are taken.

## CONSTRUCTORS IN DERIVED CLASSES

A derived class does not inherit the constructors of its base class. However, when defining a constructor for the derived class, you can and should include a call to a constructor of the base class (within the initialization section of the constructor definition).

If you do not include a call to a constructor of the base class, then the default (zero-argument) constructor of the base class will automatically be called when the derived class constructor is called.

## USE OF PRIVATE MEMBER VARIABLES FROM THE BASE CLASS

An object of the class HourlyEmployee (Displays 14.3 and 14.5) inherits a member variable called name from the class Employee (Displays 14.1 and 14.2). For example, the following would set the value of the member variable name of the object joe to "Josephine" (it also sets the member variable ssn to "123-45-6789" and both wageRate and hours to 0):

```
HourlyEmployee joe("Josephine", "123-45-6789", 0, 0);
```

If you want to change joe.name to "Mighty-Joe", you can do so as follows:

```
joe.setName("Mighty-Joe");
```

You must be a bit careful about how you manipulate inherited member variables such as name. The member variable name of the class HourlyEmployee was inherited from the class Employee, but the member variable name is a private member variable in the definition of the class Employee. That means that name can only be directly accessed within the definition of a member function in the class Employee. A member variable (or member function) that is private in a base class is not accessible by name in the definition of a member function for any other class, not even in a member function definition of a derived class. Thus, although the class HourlyEmployee does have a member variable named name (inherited from the base class Employee), it is illegal to directly access the member variable name in the definition of any member function in the class definition of HourlyEmployee.

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

![](img/9505fd46e120aa9c1406715936ff6251_590_0.png)

