```
{
    return m_Length*m_Width*m_Height;
}

private:
    double m_Length;            // Length of a box in inches
    double m_Width;             // Width of a box in inches
    double m_Height;            // Height of a box in inches
};

int main()
{
    CBox match(2.2, 1.1, 0.5);    // Declare match box
    CBox box2;                   // Declare box2 - no initial values

    cout << endl
         << "Volume of match = "
         << match.Volume();

    // Uncomment the following line to get an error
    // box2.m_Length = 4.0;

    cout << endl
         << "Volume of box2 = "
         << box2.Volume();

    cout << endl;
    return 0;
}
```

# How It Works

The definition of the CBox class now has two sections. The first is the public section containing the constructor and the member function Volume(). The second section is specified as private and contains the data members. Now the data members can only be accessed by the member functions of the class. You don’t have to modify any of the member functions — they can access all the data members of the class anyway. If you uncomment the statement in the function main() that assigns a value to the m_Length member of the object box2, however, you’ll get a compiler error message confirming that the data member is inaccessible. If you haven’t already done so, take a look at the members of the CBox class in Class View; you’ll see that the icon alongside each member indicates its accessibility; a small padlock in the icon shows when a member is private.

> A point to remember is that using a constructor or a member function is now the only way to get a value into a private data member of an object. You have to make sure that all the ways in which you might want to set or modify private data members of a class are provided for through member functions.

You can also put functions into the private section of a class. In this case, they can only be called by other function members of the same class. If you put the function Volume() in the private section, you will get a compiler error from the statements that attempt to use it in the function main(). If you put the constructor in the private section, you won’t be able to declare any objects of the class type.