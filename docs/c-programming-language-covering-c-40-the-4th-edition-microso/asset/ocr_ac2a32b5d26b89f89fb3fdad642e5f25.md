This last overload caused problems, as it does a different thing. For example,

```
"Joshua, Hannah, Joseph".IndexOf("Hannah");// Returns 7
```

but

```
"Joshua, Hannah, Joseph".IndexOf(new char [] {'H','a','n','n','a','h'});
// Returns 3
```

In this case, it would be better to give the overload that does something a different name:

```
public class String {
    public int IndexOf (string value);
    // Returns the index of value within this instance
    public int IndexOf (char value);
    // Returns the index of value within this instance
    public int IndexOfAny(char [] value);
    // Returns the first index of any of the
    // characters in value within the current instance
}
```

> BILL WAGNER Method overloading and inheritance don’t mix very well. Because overload resolution rules sometimes favor methods declared in the most derived class, that can sometimes mean a method declared in the derived class may be chosen instead of a method that appears to be a better match in the base class. For that reason, I recommend not overloading members that are declared in a base class.

# 1.6.7 Other Function Members

Members that contain executable code are collectively known as the function members of a class. The preceding section describes methods, which are the primary kind of function members. This section describes the other kinds of function members supported by C#: constructors, properties, indexers, events, operators, and destructors.

The following table shows a generic class called List<T>, which implements a growable list of objects. The class contains several examples of the most common kinds of function members.