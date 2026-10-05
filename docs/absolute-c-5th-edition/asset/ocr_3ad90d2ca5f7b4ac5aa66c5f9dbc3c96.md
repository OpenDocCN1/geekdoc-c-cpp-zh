# CHAPTER 14 Inheritance

> TIP: A Class Has Access to Private Members of All Objects of the Class

Consider the following lines from the implementation of the overloaded assignment operator in Display 14.13:

```
usedB = rightSide.usedB;
for (int i = 0; i < usedB; i++)
  b[i] = rightSide.b[i];
```

You might think that rightSide.usedB and rightSide.b[i] are illegal since usedB and b are private variables of some other than the calling object. Normally that objection would be correct, the object rightSide is of the same type as the class being defined, so this is legal.

In the definition of a class, you can access private members of any object of the class, not just private members of the calling object. ■

> TIP: "Is a" versus "Has a"

Early in this chapter we defined a derived class HourlyEmployee using the class Employee as the base class. In such a case object of the derived class HourlyEmployee is also of type Employee. Stated more simply, an HourlyEmployee is an employee. This is an example of the "is a relationship between classes. It is one way to make a more complex class from a simpler class.

Another way to make a more complex class from a simpler class is known as the "has a" relationship. For example

In most situations, you can make your code work with either an "is a" or a "has a" relationship. It seems silly (and is silly) to make the PassengerAirplane class a derived class of the JetEngine class, but it can and be made to work (perhaps with difficulty). The best programming technique is to simply follow what sounds most natural in English. It makes more sense to say "A passenger airplane has a jet engine" than to say "A passenger airplane is a jet engine.\ So, it makes better programming to have JetEngine as a member variable of a PassengerAirplane class. It makes little sense to make the PassengerAirplane class a derived class of the JetEngine class. ■