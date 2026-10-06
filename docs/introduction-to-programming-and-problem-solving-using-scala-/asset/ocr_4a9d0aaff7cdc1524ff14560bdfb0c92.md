# Case Classes

In this call it is explicit what values are going to parameters. One advantage of is you can enter the arguments in a different order. For example, you might inadvertently think that x was the first argument instead of the last. Without named arguments, this would lead to an error with no error message. You would simply get the wrong answer. If you use named arguments it is fine because names supersede the order.

```
scala evalQuadratic(x=5, a=2, b=3, c=4)
res5: Double = 69.0
```

We see that even though x is first, the value is correct.
You can use named parameters without naming all the parameters. You can start the list with arguments that are based on position and use names for the ones later. All arguments after the first one have to be named, and they cannot duplicate any that you gave using the position.

For some functions, there are arguments that will provide a particular value of that. For example, if you were creating a program to help a local bank calculate loans, it might be likely that most of their customers live in the same state. In that case it is nice to make it so that calling the function does not have to provide a value for the state and let the function use a DEFAULT VALUE. When you declare the function simply follow the type with an equals sign and the value you want for the default. If the caller calls with the default value, then argument can be left out. Default arguments are in the middle then you will have to use named arguments to specify any arguments after them in the list. Consider a function to add a grade to a Student

```
def addGrade(name:String, grade:Int = 0):Student = ...
```

Here the default grade is a zero. This function can be called in two ways.

```
addGrade("Quinn", 95)
addGrade("Kyle")
```

The first call is everything we have to this point. The second one leaves off the grade. As a result, Kyle gets a 0 for whatever grade this was.

# 10.2.4 The copy Method

The fact that you cannot mutate the values in a case class means that it would be helpful to have a way to make new case class objects that are only slightly different from existing instances. To see this, consider what happens when you want to add a new grade to a Student. The grades are in Lists, and it is easy to add to a List. The problem is, that does not mutate in the original List, it gives you a new List that includes the new values as what was already there.

To help around this problem, case classes come with a copy method. The copy method is intended to be used with the named arguments that were discussed in section 10.2.3. The arguments to copy have the same names as the fields in the class. Using named arguments, you only provide the ones you want to change. Anything you leave out will be copied straight over to the new object. So using the Student object we gave the name s above, we could use copy to do the following.