# Constructors 279

The new element on the second line of the constructor definition is called the initialization section. As this example shows, the initialization section goes after the parenthesis that ends the parameter list and before the opening brace of the function body. The initialization section consists of a colon followed by a list of or all the member variables by commas. Each member variable is followed by its initializing value in parentheses. Notice that the initializing values can be given in terms of the constructor parameters.

initialization section

The function body in a constructor definition with an initialization section need not be empty as in the previous example. For example, the following improved version of the constructor definition checks to that arguments are appropriate:

```
DayYear::DayYear(int monthValue, int dayValue)
    : month(monthValue), day(dayValue)
{
    if ((month < 1) || (month > 12))
    {
        cout << "Illegal month value!\n";n        exit(1);
    }
    if ((day < 1) || (day > 31))
    {
        cout << "Illegal day value!\n";n        exit(1);
    }
}
```

You can overload a constructor name DayYear::DayYear, just as you can overload any other member function name. In fact, constructors usually are overloaded so that objects can be initialized in more than one way. For example, in Display 7.1 we have redefined the class name DayYear so that it has three versions of its constructor. This redefinition overloads the constructor name DayYear so that it can have any arguments (as we discussed), one argument, or no arguments.

Notice that in Display 7.1, constructors call the member function test check that their initialized values are appropriate. The member function test is private since it is only intended to be used by other member functions and is part of the hidden implementation details.

We have omitted the member function set from this class definition of DayYear. Once you have a good set of constructor definitions, there is no need for any other member functions to set the member variables of the class. You can use the constructor DayYear in Display 7.1 for the same purposes that you would use the member function set (which we included in the old version of the class shown in Display 6.4).