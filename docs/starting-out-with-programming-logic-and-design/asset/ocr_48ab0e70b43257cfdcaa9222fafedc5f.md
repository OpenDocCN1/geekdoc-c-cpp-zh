# Review Questions

Although these examples are very simple, polymorphism has many practical uses. For example, a university's software processes a lot of data about students, so it might use a Student class. One of the methods in the Student class might be called getFees. This method would return the amount of a typical student's fees for a biology student.

In addition, the software might have a BiologyStudent as a subclass of the Student class (because a biology student is a student). Because of additional lab charges, a biology student's fees are usually more than those of the typical student. So, the BiologyStudent class would have its method that returns the fees for a biology student.

![](bbox=[0.188, 0.267, 0.225, 0.298])

# Checkpoint

14.25 Look at the following pseudocode class definitions:

```
Class Vegetable
  Public Module message()
  Display "I'm a vegetable."
End Class
Class Potato Extends Vegetable
  Public Module message()
  Display "I'm a potato."
End Class
```

Given these definitions, what will the following pseudocode do?

```
Declare Vegetable v
Declare Potato p
Set v = New Potato()
Set p = New Potato()
Call v.message()
Call p.message()
```

# Review Questions

# Multiple Choice

+   1. A(n) \__________ programming practice is centered on creating modules and functions
that are separate from the data they work on.

+   a. modular
b. procedural
c. functional
d. object-oriented

+   2. A(n) \__________ programming practice is centered on creating objects.

+   a. object-centric
b. objective
c. procedural
d. object-oriented