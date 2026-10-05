# 17.6. FINE TUNING INHERITANCE

```
##
##
##
------
####
####
####
####
####
####
####
######
######
####
####
####
####
####
####
```

The **DrawableRectangle::draw** method needs access to the fields **length** and **width** to be able to draw the rectangle. It is important to remember that every **DrawableRectangle** object contains these fields because it inherits them from **Rectangle**, however, if the **length** and **width** fields were declared private instead of protected in **Rectangle, DrawableRectangle::draw** would not be able to access these fields.

+   A class supports three levels of protection for its members:
1. **private**: This is the default. Private members are accessible to any code within the class itself but are inaccessible to code outside of the class.
2. **protected**: Protected members are accessible to code within the class itself and to code within derived classes that use public inheritance. Protected members are inaccessible to other (non-derived) classes.
3. **public**: Public members are accessible to code anywhere.

In sum, private means not accessible outside the class, period. Public means open to everyone. Protected means “public” to subclasses and “private” to all other classes.

# 17.6 Fine Tuning Inheritance

Recall the fairly sorting code in Listing 16.5 (loggingflexible.cpp). It uses objects to enable the following functionality: