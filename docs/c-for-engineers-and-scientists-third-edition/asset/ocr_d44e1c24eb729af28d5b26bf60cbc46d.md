# Chapter 11

# 623

```
cout << "The initial date is \
```

Program 11.8 produces the following output:

```
The initial date is 04/01/07
The new date is 01/15/08
```

# Operator Functions as Friends

The operator functions in Programs 11.7 and 11.8 have been constructed as class members. An interesting feature of operator functions is that, except for the operator functions =, (), [], and ->, they can also be written as friend functions. For example, if the operator+() function used in Program 11.8 is written as a friend function, the following is a suitable declaration prototype:

```
friend Date operator+(Date&, int);
```

Notice that the friend version contains a reference to a Date object that isn't in the member function version. In all cases, the friend version of a member operator function must contain an additional class reference that the member function does not require. Table 11.2 lists this equivalence for both unary and binary operators.

# Table 11.2 Operator Function Argument Requirements

| Operator | Member Function | Friend Function |
| --- | --- | --- |
| Unary | 1 implicit | 1 explicit |
| Binary | 1 implicit and 1 explicit | 2 explicit |

Program 11.8's operator+() function, written as a friend function, is as follows:

```
Date operator+(Date& opl, int days)
{
  Date temp; // a temporary Date to store the result
  temp.day = opl.day + days; // add the days
  temp.month = opl.month;
  temp.year = opl.year; // now adjust the months
  while (temp.day > 30)
}
```

![](bbox=[0.852, 0.868, 0.876, 0.883])

> The extra argument is needed to identify the correct object. This argument isnt necessary with a member function because the functions "knows" which object it operating on. The mechanism of "knowing" is supplied by an implied member function argument