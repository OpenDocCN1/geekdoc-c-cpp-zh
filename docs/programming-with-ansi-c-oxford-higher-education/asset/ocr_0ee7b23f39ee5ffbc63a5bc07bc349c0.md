+   1. CSStudent
+   2. CSStudent ITStudent
+   3.
+   4.

![](bbox=[0.05, 0.32, 0.35, 0.55])

# Fig. 1.12 Steps for designing classes using a bottom-up approach

# Steps for designing classes using a bottom-up approach

+   1. We have the CSStudent class defined first
+   2. Now we have CSStudent as well as ITStudent
+   3. Finding out common attributes and generating student class from it
+   4. It helps in defining CEStudent

example, all horses have tails but bobtails (a type of horse) do not have any. Similarly, all birds fly but ostriches do not. Such instances are called exceptions, which need no further exploration). There are many advantages in the bottom-up design. Some are listed as follows:

+   1. There is no redundancy. The student’s name is kept only in the Student class. If we need to change the size or type of the name, we have to change at only one place, the Student class, and nowhere else. As other classes inherit from this class, all of them have the effect of the change automatically.

Hence, there are less chances of ambiguity. Assume that we are not using the base class approach. It is quite possible that the same attribute in two different classes have two different names. Suppose in one class the name of the student is defined as StudName, in the second class the name is defined as Name, and the third class probably calls it StudentName. More than one class representing the same real-world entity or more than one attribute name referring to the same attribute creates a lot of ambiguity in the designer’s and developer’s mind. This is eliminated here as there is a single class, and the name given to the attribute student name (say StudNm) is the same in all classes because these classes do not define this attribute themselves, but they just inherit them.

> Note In C++, we need to recompile the program when the base class changes itself. We need to recompile the program even when the program is not changed a bit. This is not a flaw in the design. Read Section 9.6 in Chapter 9 for finding out the reason.

+   2. Adding a new attribute to all the classes is simple. Suppose we would like to add mobile number as an additional attribute to all three classes, we can do it by placing it in the Student class. We do not need to pick each class one by one and do it individually.

This example, as mentioned earlier, introduces the concept of the bottom-up design. There are sound reasons to follow the bottom-up design approach in many cases.

Let us concentrate now on the class that is generated as a side effect of the design. The class that now contains the shared attributes becomes the base class for all such classes under consideration. This base class, interestingly, is the abstract class. Why? There is nobody who is only student; we may have a CSStudent, a CEStudent, or an ITStudent, but nobody is just a student. Hence, the student class in this design is an abstract class. We are not going to define any object of the class Student.