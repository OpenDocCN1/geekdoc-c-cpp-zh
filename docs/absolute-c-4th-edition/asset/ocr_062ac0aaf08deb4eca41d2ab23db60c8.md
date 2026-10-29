```
82        case 11:
83            cout << "November "; break;
84        case 12:
85            cout << "December "; break;
86        default:
87            cout << "Error in DayOfYear::output. Contact software vendor.";
88    }

89    cout << day;
90 }
```

# SAMPLE DIALOGUE

```
Testing the class Holiday.
February 14
Parking laws will be enforced.
```

The notation date(month, day) is an invocation of the constructor for the class DayOfYear with arguments month and day to initialize the member variables of date. Notice that this notation is analogous to how you would declare a variable data of type DayOfYear. Also notice that the parameters of the larger class constructor Holiday can be used in the invocation of the constructor for the member variable.

# 7.2  More Tools

> > Intelligence . . . is the facility of making artificial objects, especially tools
> > to make tools.
> >
> > — Henri Bergson, *Creative Evolution*

This section discusses three topics that, although important, did not fit easily before here. The three topics are const parameters for classes, inline functions, and static class members.

# THE const PARAMETER MODIFIER

A call-by-reference parameter is more efficient than a call-by-value parameter. A call-by-value parameter is a local variable that is initialized to the value of its argument, so when the function is called there are two copies of the argument. With a call-by-reference parameter, the parameter is just a placeholder that is replaced by the argument, so there is only one copy of the argument. For parameters of simple types, such as int or double, the difference in efficiency is negligible, but for class parameters the difference in