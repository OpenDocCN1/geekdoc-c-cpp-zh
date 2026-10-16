```
{
    cout << "(" << aGenericPlayer.GetTotal() << ")";
}
}
else
{
    os << "<empty>";
}
return os;
}
```

The function displays the generic player’s name and cards, along with the total value of the cards.

# SUMMARY

In this chapter, you should have learned the following concepts:

+   - One of the key elements of OOP is inheritance, which allows you to derive a new class from an existing one. The new class automatically inherits data members and member functions from the existing class.
+   - A derived class does not inherit constructors, copy constructors, destructors, or an overloaded assignment operator.
+   - Base class constructors are automatically called before the derived class constructor when a derived class object is instantiated.
+   - Base class destructors are automatically called after the derived class destructor when a derived class object is destroyed.
+   - Protected members are accessible only in their own class and certain derived classes, depending upon the derivation access level.
+   - Using public derivation means that public members in the base class become public members in the derived class, protected members in the base class become protected members in the derived class, and private members are (as always) inaccessible.
+   - You can override base class member functions by giving them new definitions in a derived class.
+   - You can explicitly call a base class member function from a derived class.