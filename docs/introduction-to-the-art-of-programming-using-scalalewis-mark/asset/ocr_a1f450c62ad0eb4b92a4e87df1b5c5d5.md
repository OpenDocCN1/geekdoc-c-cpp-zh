```
res2: Double = 69.0
```

In this call it is now explicit what values are going to what parameters. One advantage of this is when you enter the arguments in a different order, the meaning will be what you want. For example, you might think that x was the first argument instead of the last. Without names arguments, this would lead to an error with no error message. You would simply get the wrong answer. However, if you use named arguments everything is fine because the names supersede the order.

```
scala> evalQuadratic(x=5,a=2,b=3,c=4)
res3: Double = 69.0
```

Here we see that even though x is first, the value we get is correct.

You can use named parameters without naming all the parameters. You can start the list with arguments that are based on position and then use names for the later ones. All the arguments after the first named one have to be named and they can not duplicate any that you gave using the position.

For some functions there are some arguments that will have a particular value a lot of the time. In that situation, it is nice to make it so that people calling the function do not have to provide them and they will use a DEFAULT VALUE. When you declare the function simply follow the type with an equals sign and the value you want to have for the default. If the caller is happy with the default value, then that argument can be left out. Default arguments at the end of the list can be simply omitted. If they are in the middle then you will have to use named arguments to specify any arguments after them in the list. Consider a function to add a grade to a Student.

```
def addGrade(name:String,grade:Int = 0):Student = ...
```

Here the default grade is a zero. So this function can be called in two ways.

```
addGrade("Jane",95)
addGrade("Joe")
```

The first call is like everything we have seen to this point. The second one leaves off the grade. As a result, Joe gets a 0 for whatever grade this was.

# 10.2.4 The copy Method

The fact that you can not mutate the values in a case class means that it would be helpful to have a way to make new case class objects that are only slightly changed from others. To see this, consider what happens when you want to add a new grade to a Student. The grades are in Lists, and it is easy to add to a List. The problem is, that does not mutate what is in the original List, it just gives us a new List that includes the new values as well as what was already there.

To help get around this problem, case classes come with a copy method. The copy method is intended to be used with the named arguments that were discussed in section 10.2.3. The arguments to copy have the same names as the fields in the class. Using named arguments, you only provide the ones you want to change. Anything you leave out will be copied straight over to the new object. So using the Student object we gave the name s above, we could use copy to do the following.