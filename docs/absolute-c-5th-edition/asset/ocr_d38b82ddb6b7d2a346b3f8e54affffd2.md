# Inheritance Basics

# 625

# An Object of a Derived Class Has More One Type

In everyday, an hourly employee is an employee. In C++, the same sort of thing holds. Since HourlyEmployee is a derived class of the class Employee, every object of the class HourlyEmployee can be used anyplace of the class Employee can be used. In particular, you can use an argument of type HourlyEmployee when a function requires an argument of type HourlyEmployee. You can assign a plain old HourlyEmployee object to a variable of type HourlyEmployee. After all, an Employee is not necessarily an HourlyEmployee.) Of course, the same remarks apply to any base class and its derived class. You can use an object of a derived class anyplace that its base class is allowed.

More generally, an object of a class type can be used anyplace of any of its ancestor classes can be used. If class Child is derived from Ancestor and class grandchild is derived from class Child, then an object of class Grandchild can be used anyplace an object of class Child can be used, and the object of class Grandchild can also be used anyplace that an object of class Ancestor can be used.

In this constructor definition, the default (zero-argument) version of the base class constructor is called to initialize the inherited member variables. You should always include an invocation of one of the base class constructors in the initialization section of a derived class constructor

If a constructor for a derived class does not include an invocation of a constructor for the base class, then the default (zero-argument) version of the base class constructor will be invoked automatically. So, the following definition of the default constructor for the class HourlyEmployee (with Employee( omitted) is equivalent to the version we just discussed:

```
HourlyEmployee::HourlyEmployee( ) : wageRate(0), hours(0)
{
    //iberately empty
}
```

However, prefer to explicitly include a call to a base class constructor, even if it would be invoked automatically.
A derived class has all the member variables of the base class. When a derived class constructor is called, these member variables need to be allocated and should be initialized. This allocation of memory for the inherited member variables must be done by a constructor for the base class, and the base constructor is the most convenient place to initialize these inherited member variables. That is why you should always include a call to one of the base class constructors when you define a constructor for a derived class. If you do not include a call to a base class constructor (in the initialization section of the derived class constructor), the default constructor is called automatically. (If there is no default constructor for the base class, an error occurs.)