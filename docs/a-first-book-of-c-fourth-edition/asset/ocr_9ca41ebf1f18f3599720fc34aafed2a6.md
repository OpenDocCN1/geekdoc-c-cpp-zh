To retain restricted access across derived classes, C++ provides a third access specification—protected. Protected access behaves the same as private access, in that it permits access only to member or friend functions, but it allows any derived class to inherit this restriction. The derived class then defines the type of inheritance it’s willing to take on, subject to the base class’s access restrictions. This definition is done by the class access specifier, which is listed after the colon at the start of the class declaration section. Table 12.1 lists the derived class member access resulting from the base class’s member specifications and the derived class access specifier.

The shaded rows in Table 12.1 show that if the base class member has a protected access and the derived class access specifier is public, the derived class member is protected to its class. Similarly, if the base class has a public access and the derived class access specifier is public, the derived class member is public. These specifications for base class data members and member functions are the most commonly used, so they’re the ones used in this section. So for all classes intended for use as a base class, a protected data member access is used instead of a private designation.

# Table 12.1 Inherited Access Restrictions

| Base Class Member | Derived Class Access Specifier | Derived Class Member |
|---|---|---|
| private | : private | inaccessible |
| protected | : private | private |
| public | : private | private |
| private | : public | inaccessible |
| protected | : public | protected |
| public | : public | public |
| private | : protected | inaccessible |
| protected | : protected | protected |
| public | : protected | protected |

# An Example

To understand how to derive one class from another, examine the process of deriving the Cylinder class from the base class Circle. The definition of the Circle class is as follows:

```
// class declaration section
class Circle
{
    protected:
        double radius;
    public:
        Circle(double = 1.0); // constructor
        double calcval();
};
```