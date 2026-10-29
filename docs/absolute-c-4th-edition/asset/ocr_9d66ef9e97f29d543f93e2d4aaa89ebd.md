```
return Money(finalDollars, finalCents);
```

The expression that is returned is an invocation of the constructor for Money. Although we sometimes think of a constructor as a void function, a constructor constructs an object and can also be thought of as returning an object of the class. If you feel uncomfortable with this use of the constructor, it may help to know that this return statement is equivalent to the following, more cumbersome and less efficient, code:

```
Money temp;
temp = Money(finalDollars, finalCents);
return temp;
```

An expression, such as Money(finalDollars, finalCents), is sometimes called an **anonymous object**, since it is not named by any variable. However, it is still a full-fledged object. You can even use it as a calling object, as in the following:

```
Money(finalDollars, finalCents).getDollars()
```

The previous expression returns the int value of finalDollars.

# Self-Test Exercises

+   1. What is the difference between a (binary) operator and a function?
+   2. Suppose you wish to overload the operator < so that it applies to the type Money defined in Display 8.1. What do you need to add to the definition of Money given in Display 8.1?
+   3. Is it possible using operator overloading to change the behavior of + on integers? Why or why not?

# RETURNING BY const VALUE

Notice the returned types in the declarations for overloaded operators for the class Money in Display 8.1. For example, the following is the declaration for the overloaded plus operator + as it appears in Display 8.1:

```
const Money operator +(const Money& amount1, const Money& amount2);
```

This subsection explains the const at the start of the line. But before we discuss that first const, let’s make sure we understand all the other details about returning a value. So, let’s first consider the case where that const does not appear in either the declaration or