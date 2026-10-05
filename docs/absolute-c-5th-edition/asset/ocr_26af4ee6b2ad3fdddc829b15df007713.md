The call to the base constructor is the first action taken by a derived class. Thus, if class B is derived from class A and class C is derived from class B, then when an object of class C is created, first a constructor for class A is called, then a constructor for B is called, and finally the remaining actions of the class C constructor are taken.

# Constructors in Derived Classes

A derived class does not inherit the constructors of its base class. However, when defining a constructor for the derived class, you can and should include a call to a constructor of the base class (within the initialization section of the constructor).

If you do not include a call to a constructor of the base class, then the default (zero-argument) constructor of the base class will be called when the derived class constructor is called.

# PITFALL: Use of Private Member Variables from the Base Class

![](bbox=[0.125, 0.458, 0.193, 0.492])

An object of a class HourlyEmployee (Displays 14.3 and 14.5) has a member variable named name from the class Employee (Displays 14.1 and 14.2). For example, the following would set the value of the member variable name of the object joe to "Josephine" (it also sets the member variable name to "123-45-6789" and both wageRate and hours to 0):

```
HourlyEmployee joe("Josephine", "123-45-6789", 0, 0);
```

If you want to change joe.name to "Mighty-Joe", you can do so as follows:

```
joe.setName("Mighty-Joe");
```

You must be careful about how you manipulate inherited member variables as name. The member variable name of the class HourlyEmployee was inherited from the class Employee, but the member variable name is a private variable in the definition of the class Employee. That name can only be directly accessed within the definition of a member function in the class Employee. A member variable (or member function) that is private in a base class is not accessible by the definition of a member function for any other class, not even in a member function of a derived class. Thus, although the class HourlyEmployee has a member variable named name (inherited from the base class Employee), it is illegal to directly access the member variable in the definition of any member function in the class definition of HourlyEmployee.