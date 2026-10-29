Following the private class data members, the method prototypes listed in the Date class have been declared as public. This means these class methods can be called by any objects and functions not in the class (from outside the class, in other words). In general, all class methods should be public so that they provide capabilities to manipulate class variables from outside the class.

The Date class provides three methods named Date(), setDate(), and showDate(). Notice that one of these member methods has the same name, Date, as the class name. It’s referred to as a constructor method, and it has a special purpose: It can be used to initialize class data members with values. The default values used for this method are the numbers 7, 4, and 2012, which, as you see shortly, are used as the default month, day, and year values. Note that the default year is represented as a four-digit integer to retain the century designation. Also, notice that the constructor method has no return type, which is a requirement for this special method. The two remaining methods declared in the Date class, setDate() and showDate(), have been declared as returning no value (void).

The class implementation section is where the member methods declared in the declaration section are written to permit the initialization, assignment, and display capabilities implied by their names. The following example shows the general form of methods written in the implementation section. This format is correct for all methods except the constructor, which, as stated previously, has no return type:

```
returnType className::methodName(parameter list)
{
    method body
}
```

As this example shows, member methods defined in the class implementation section have the same format as all user-written C++ functions, with the addition of the class name and scope resolution operator, ::, that identifies the method as a member of a particular class. Now take another look at the implementation section of the Date class, which is repeated for convenience:

```
// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}
```