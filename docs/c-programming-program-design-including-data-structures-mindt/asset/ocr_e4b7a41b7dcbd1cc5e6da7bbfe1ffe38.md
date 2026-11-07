The statement in Line 18 uses the object `illusObject2` and the function `incrementY` to increment `y`. The statement in Line 19 sets the value of the member variable `x` of `illusObject2` to 23. Lines 20 and 21 output the data stored in the objects `illusObject1` and `illusObject2`. Notice that the value of `y` for both objects is the same. Similarly, the value of `count` for both objects is the same. Moreover, notice that the statement in Line 19 changes only the value of the member variable `x` of `illusObject2`, because `x` is *not a static member* of the class `illustrate`.

> > **NOTE**
> >
> > Here are some additional comments on `static` members of a class. As you have seen in this section, a `static` member function of a class does not need any object to be invoked. It can be called using the name of the class and the scope resolution operator, as illustrated. Therefore, a `static` member function cannot use anything that depends on a calling object. In other words, in the definition of a `static` member function, you cannot use a non-`static` member variable or a non-`static` function unless there is an object declared locally that accesses the non-`static` member variable or the non-`static` member function.

Let us again consider the class `illustrate`, as defined in Example 10-12. This class contains both `static` and non-`static` member variables. When we declare objects of this class, each object has its own copy of the member variable `x`, which is non-`static`, and all objects share the member variables `y` and `count`, which are `static`. Earlier in this chapter, we defined the terminology instance variables of a class using the class `clockType`. However, at that point, we did not discuss `static` member variables of a class. A class can have `static` as well as non-`static` member variables. We can, therefore, make the general statement that non-`static` member variables of a class are called the instance variables of the class.

# ## PROGRAMMING EXAMPLE: Juice Machine

![](bbox=[0.081, 0.642, 0.139, 0.712])

A common place to buy juice is from a machine. A new juice machine has been purchased for the gym, but it is not working properly. The machine sells the following types of juices: orange, apple, mango, and strawberry-banana. You have been asked to write a program for this juice machine so that it can be put into operation.

The program should do the following:

+   1. Show the customer the different products sold by the juice machine.
+   2. Let the customer make the selection.
+   3. Show the customer the cost of the item selected.