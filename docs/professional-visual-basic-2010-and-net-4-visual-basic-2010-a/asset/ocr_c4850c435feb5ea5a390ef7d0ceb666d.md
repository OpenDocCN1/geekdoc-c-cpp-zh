parts of your application. To determine what is going on with spaghetti code, you must trace through many routines and mentally piece together what it all means.

Object-oriented programming can help you avoid this problem, but it is most definitely not a magic bullet. In fact, when you create deep inheritance hierarchies, you are often creating spaghetti code because each level in the hierarchy not only extends the previous level’s interface, but almost always also adds functionality. Thus, when you look at the final `NATFACustomer` class, it may have very little to do. To figure out what it does or how it behaves, you have to trace through the code in the previous four levels of classes, and you might not even have the code for some of those classes, as they might come from other applications or class libraries you have purchased.

On the one hand, you have the benefit of reusing code; but on the other hand, you have the drawback that the code for one object is actually scattered through five different classes. Keep this in mind when designing systems with inheritance — use as few levels in the hierarchy as possible to provide the required functionality.

# The Fragile-Base-Class Problem

You have explored where it is appropriate to use inheritance and where it is not. You have also explored how you can use inheritance and multiple interfaces in conjunction to implement both is-a and act-as relationships simultaneously within your classes.

Earlier, I noted that while inheritance is an incredibly powerful and useful concept, it can also be very dangerous if used improperly. You have seen some of this danger in the discussion of the misapplication of the is-a relationship, and how you can use multiple interfaces to avoid those issues.

One of the most classic and common problems with inheritance is the fragile base-class problem. This problem is exacerbated when you have very deep inheritance hierarchies, but it exists even in a single-level inheritance chain.

The issue you face is that a change in the base class always affects all child classes derived from that base class. This is a double-edged sword. On the one hand, you get the benefit of being able to change code in one location and have that change automatically cascade through all derived classes. On the other hand, a change in behavior can have unintended or unexpected consequences farther down the inheritance chain, which can make your application very fragile and hard to change or maintain.

# Interface Changes

There are obvious changes you might make, which require immediate attention. For example, you might change your `Contact` class to have `FirstName` and `LastName` instead of simply `Name` as a property. In the `Contact` class, replace the `mName` variable declaration with the following code:

```
Private mFirstName As String
Private mLastName As String
```

Now replace the Name property with the following code:

```
Public Property FirstName() As String
    Get
        Return mFirstName
    End Get
    Set(ByVal value As String)
        mFirstName = value
    End Set
End Property
Public Property LastName() As String
    Get
        Return mLastName
    End Get
    Set(ByVal value As String)
```