As the comments indicate, you cannot place the three lines shown in your program. The first line can be made to acceptable, but the two calls to the constructor DayOfYear are illegal. A constructor cannot be called in the same name as an ordinary member function. Still, it is clear what we want to happen when we write those three lines, and that happens automatically when you declare the objects date1 and date2 as follows:

```
DayOfYear date1(7, 4), date2(5, 5);
```

The definition of a constructor is in the same way as any other member function. For example, if you revise the definition of the class DayOfYear by adding the constructor just described, you need to add a definition of the constructor, which might be as follows:

```
DayOfYear::DayOfYear(int monthValue, int dayValue)
    month = monthValue;
    day = dayValue;
```

Since the class and the constructor have the same name, the name DayOfYear occurs twice in the function heading: the DayOfYear before the scope resolution operator :: is the name of the class, and the DayOfYear after the scope resolution operator is the name of the constructor function. Also notice that no return type is specified in the heading of the constructor definition, not even the type void. Aside from these points, a constructor can be defined in the same way as an ordinary member function.

A constructor is a member function of a class that has the same name as the class. A constructor is called automatically when an object of the class is declared. Constructors are used to initialize objects. A constructor must have the same name as the class of which it is a member.

As we just illustrated, a constructor can be defined just like any other member function. However, there is an alternative way of defining constructors that is preferable to use. The previous definition of the constructor DayOfYear is completely equivalent to the following version:

```
DayOfYear::DayOfYear(int monthValue, int dayValue)
    : month(monthValue), day(dayValue)
/*Body intentionally empty**/
```