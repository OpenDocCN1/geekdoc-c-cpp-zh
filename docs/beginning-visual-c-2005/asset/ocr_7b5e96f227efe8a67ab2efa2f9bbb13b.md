The output shows that all the constructors and destructors are called in the correct sequence and the copy constructor for the CBox part of chocolateBox is called before the CCandyBox copy constructor. The volume of the object chocolateBox of the derived class is now the same as that of its initializing object, which is as it should be.

You have, therefore, another golden rule to remember:

> If you write any kind of constructor for a derived class, you are responsible for the initialization of all members of the derived class object, including all its inherited members.

# Class Members as Friends

You saw in Chapter 7 how a function can be declared as a friend of a class. This gives the friend function the privilege of free access to any of the class members. Of course, there is no reason why a friend function cannot be a member of another class.

Suppose you define a CBottle class to represent a bottle:

```
class CBottle
{
public:
    CBottle(double height, double diameter)
    {
        m_Height = height;
        m_Diameter = diameter;
    }

private:
    double m_Height;            // Bottle height
    double m_Diameter;          // Bottle diameter
};
```

You now need a class to represent the packaging for a dozen bottles that automatically has custom dimensions to accommodate a particular kind of bottle. You could define this as:

```
class CCarton
{
public:
    CCarton(const CBottle& aBottle)
    {
        m_Height = aBottle.m_Height;        // Bottle height
        m_Length = 4.0*aBottle.m_Diameter;  // Four rows of ...
        m_Width = 3.0*aBottle.m_Diameter;   // ...three bottles
    }

private:
    double m_Length;    // Carton length
    double m_Width;     // Carton width
    double m_Height;    // Carton height
};
```