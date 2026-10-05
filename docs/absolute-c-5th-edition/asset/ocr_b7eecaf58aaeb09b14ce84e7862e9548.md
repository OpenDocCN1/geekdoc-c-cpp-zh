# 294 CHAPTER 7 Constructors and Other Tools

Display 7.3 A Class Member Variable (part 3 of 31)

```
84    case 12:
85        cout << "December \ break;
86    default:
87        cout << "Error in DayOfYear::output.";
88
89    cout << day;
90 }
```

Sample Dialogue

Testing the class Holiday.
February 14
Parking laws will be enforced.

The class Holiday in Display 7.3 might be used by some police departments to help keep track of holidays will have parking enforcement(of things as parking meters and one hour parking zones). It is a highly simplified class. A real class would have more member functions, but the class Holiday is complete enough to illustrate our points.

The class has two member variables. The member variable parking Enforcement is an ordinary member variable of the simple type bool. The member variable is of the class type DayOfYear.

We have replaced one constructor definition from Display 7.3:

```
Holiday::Holiday(int month, int day, bool theEnforcement)
    : date(month, day), parkingEnforcement(theEnforcement)
    /*Intentionally empty.*/
```

Notice that we set the member variable parkingEnforcement in the initialization section in the usual way, namely,

```
parkingEnforcement(theEnforcement)
```

The member variable date is a member of the class DayOfYear. To initialize date, we need to invoke a constructor from the class DayOfYear(the type of date). This is done in the initialization section with the similar notation

```
date(month, day)
```

The notation date(month, day) is an invocation of the constructor for the class DayOfYear with arguments month and day to initialize the member variables of date. Notice that this is analogous to how you would declare a variable date of type DayOfYear. Also notice the parameters of the larger class constructor Holiday can be used in the invocation of the constructor for the member variable.