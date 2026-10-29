# Introduction to Classes

As mentioned, constructors can also be written as inline functions. Doing so simply means defining the function in the class declaration section. For example, the following declaration section makes both constructors in Program 10.3 inline:

```
```cpp
// class declaration section
class Date
{
    private:
        int month;
        int day;
        int year;
    public:
        Date(int mm = 7, int dd = 4, int yyyy = 2012)
        {
            month = mm;
            day = dd;
            year = yyyy;
        }
        Date(long yyyymmdd)   // here is the overloaded constructor
        {
            year = int(yyyymmdd/10000.0);    // extract the year
            // extract the month
            month = int((yyyymmdd - year * 10000.0)/100.00);
            // extract the day
            day = int(yyyymmdd - year * 10000.0 - month * 100.0);
        }
};
```
```

The keyword inline isn’t required in this declaration because member methods defined in the class declaration are inline by default.

Generally, only methods that can be coded on a single line are good candidates for inline functions. This guideline reinforces the convention that inline functions should be small. Therefore, the first constructor is more conventionally written as follows:

```
```cpp
Date(int mm = 7, int dd = 4, int yyyy = 2012)
{
    month = mm; day = dd; year = yyyy;
}
```
```

The second constructor, which extends over three lines, should not be written as an inline function.

# Destructors

The counterpart to constructor methods are **destructor methods**. Destructors are methods with the same class name as constructors but are preceded with a tilde (~). Therefore, for the Date class, the destructor name is ~Date(). Like constructors, the C++ compiler provides a default do-nothing destructor in the absence of an explicit destructor. Unlike constructors, however, there can be only one destructor method per class because destructors take no parameters and return no values.