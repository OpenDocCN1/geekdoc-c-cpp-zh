```
result.minutes = totalminutes % 60;
return result;
}
```

With this declaration and definition, the statement

```
A = 2.75 * B;
```

translates to the following and invokes the nonmember friend function just defined:
A = operator*(2.75, B);

In short, a friend function to a class is a nonmember function that has the same access
rights as a member function.

# Are Friends Unfaithful to OOP?

At first glance, it might seem that friends violate OOP principle of hiding because
the friend mechanism allows nonmember functions to access private data. However, that is
anarrow narrow view. Instead, you should think of friend functions as part of an extended
interface for a class. For example, from a conceptual point of view, letting a double by a
Time value is pretty much the same as multiplying a Time value by a double. The first
requires a friend function whereas the second can be done with a member function is the
result of C++ syntax, not of a deep conceptual difference. By using both friend function
and a class method, you can express either operation with the same user interface. Also
keep in mind that only a class declaration decide which functions are friends, so the
class declaration still controls which functions access private data. In short, class methods
and friends are simply two different mechanisms for expressing a class interface.

Actually, you can write this particular friend function as a non-friend by altering thendefinition so that it switches which value comes first in the multiplication:

```
Time operator*(double m, const Time & t);
{
return t * m; // use t.operator*(m)
}
```

The original version accessed t.minutes and t.hours explicitly, so it had to be a
friend. This version uses only the Time object as a whole, letting a member function
hand the private values, so this version does not have to be a friend. Nonetheless, there
are reasons to make this a friend, too. Most importantly, it ties the function in as
 of the official class interface. Second, if you later find a need for the function to access
private data directly, you only have to change the function definition and not the class
prototype.

Tip

If you want to overload an operator for a class and want to use it as a non-
class term as the first operand, you can use a friend function to reverse the operand order.