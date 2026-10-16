Manager is an Employee, with a few pieces of information added:

```
struct Manager : public Employee {
list<Employee*> group;
short level;
// ...
};
```

The Manager is derived from Employee, and conversely, Employee is a base class for Manager. The class Manager has the members of class Employee (first_name, department, etc.) in addition to its own members (group, level, etc.).

Derivation is often represented graphically by a pointer from the derived class to its base class indicating that the derived class refers to its base (rather than the other way around):

Employee
Manager

A derived class is often said to inherit properties from its base, so the relationship is also called inheritance. A base class is sometimes called a superclass and a derived class a subclass. This terminology, however, is confusing to people who observe that the data in a derived class object is a superset of the data of an object of its base class. A derived class is typically larger (and never smaller) than its base class in the sense that it holds more data and provides more functions.

A popular and efficient implementation of the notion of derived classes has an object of the derived class represented as an object of the base class, with the information belonging specifically to the derived class added at the end. For example:

Employee: Manager:

```
first_name first_name family_name family_name ... ...
group level ...
```

No memory overhead is implied by deriving a class. The space required is just the space required by the members.

Deriving Manager from Employee in this way makes Manager a subtype of Employee, so that a Manager can be used wherever an Employee is acceptable. For example, we can now create a list of Employees, some of whom are Managers:

```
void f(Manager m1, Employee e1)
{
list<Employee*> elist {&m1,&e1};
// ...
}
```

A Manager is (also) an Employee, so a Manager* can be used as an Employee*. Similarly, a Manager& can be used as an Employee&. However, an Employee is not necessarily a Manager, so an Employee* cannot be used as a Manager*. In general, if a class Derived has a public base class (§20.5) Base, then a Derived* can be assigned to a variable of type Base* without the use of explicit type conversion. The opposite