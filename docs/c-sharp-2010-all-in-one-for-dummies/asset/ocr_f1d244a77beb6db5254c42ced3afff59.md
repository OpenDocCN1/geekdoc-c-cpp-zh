# Inheritance is amazing

To make sense of their surroundings, humans build extensive taxonomies. For example, Fido is a special case of dog, which is a special case of canine, which is a special case of mammal — and so it goes. This ability to classify items shapes our human understanding of the world.

In an object-oriented language such as C#, you say that the class Student inherits from the class Person. You also say that Person is a base class of Student and that Student is a subclass of Person. Finally, you say that a Student IS_A Person. (Using all caps and an underscore is a common way of expressing this unique relationship — I didn't make up this concept.)

Notice that the IS_A property isn't reflexive: Although Student IS_A Person, the reverse isn't true. A Person IS_NOT A Student. A statement such as this one always refers to the general case. A particular Person might be, in fact, a Student — but lots of people who are members of the class Person aren't members of the class Student. In addition, the class Student has properties that it doesn't share with the class Person. For example, Student has a grade-point average, but the ordinary Person quite happily does not.

The inheritance property is transitive. For example, if I define a new class GraduateStudent as a subclass of Student, GraduateStudent is also a Person. It must be that way: If a GraduateStudent IS_A Student and a Student IS_A Person, a GraduateStudent IS_A Person.

SubClass gets all members of BaseClass as its own, plus any members it may add to the pile. Main() demonstrates that SubClass now has a data member, _dataMember, and a member method, SomeMethod(), to join the brand-new member of the family, little method SomeOtherMethod() — and what a joy it is, too.

The program produces the following expected output (I'm usually sort of surprised whenever one of my programs works as expected):

```
Exercising a base class object:
SomeMethod()
Exercising a subclass object:
SomeMethod()
SomeOtherMethod()
Press Enter to terminate...
```

# Why You Need Inheritance

Inheritance serves several important functions. You may think, for example, that inheritance reduces the amount of typing. In a way, it does — you don't need to repeat the properties of a Person when you're describing a Student class. A more important, related issue is the major buzzword reuse. Software scientists have known for some time that starting from scratch