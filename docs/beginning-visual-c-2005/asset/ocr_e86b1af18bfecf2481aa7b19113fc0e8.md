# Chapter 9

The constructor here sets the height to be the same as that of the bottle it is to accommodate, and the length and width are set based on the diameter of the bottle so that twelve fit in the box.

As you know by now, this won’t work. The data members of the CBottle class are private, so the CCarton constructor cannot access them. As you also know, a friend declaration in the CBottle class fixes it:

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

    // Let the carton constructor in
    friend CCarton::CCarton(const CBottle& aBottle);
};
```

The only difference between the friend declaration here and what you saw in Chapter 7 is that you must put the class name and the scope resolution operator with the friend function name to identify it. For this to compile correctly, the compiler needs to have information about the CCarton class constructor, so you would need to put an #include statement for the header file containing the CCarton class definition before the definition of the CBottle class.

# Friend Classes

You can also allow all the function members of one class to have access to all the data members of another by declaring it as a friend class. You could define the CCarton class as a friend of the CBottle class by adding a friend declaration within the CBottle class definition:

```
friend CCarton;
```

With this declaration in the CBottle class, all function members of the CCarton class now have free access to all the data members of the CBottle class.

# Limitations on Class Friendship

Class friendship is not reciprocated. Making the CCarton class a friend of the CBottle class does not mean that the CBottle class is a friend of the CCarton class. If you want this to be so, you must add a friend declaration for the CBottle class to the CCarton class.

Class friendship is also not inherited. If you define another class with CBottle as a base, members of the CCarton class will not have access to its data members, not even those inherited from CBottle.