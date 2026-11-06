# Section 9.15 *static* Class Members

+   - A `static` **data member** (p. 429) represents “classwide” information (i.e., a property of the class shared by all instances, not a property of a specific object of the class).
+   - `static` data members have class scope and can be declared `public`, `private` or `protected`.
+   - A class’s `static` members exist even when no objects of that class exist.
+   - To access a `public static` class member when no objects of the class exist, simply prefix the class name and the scope resolution operator (`::`) to the name of the data member.
+   - The `static` keyword cannot be applied to a member definition that appears outside the class definition.
+   - A member function should be declared `static` (p. 430) if it does not access non-`static` data members or non-`static` member functions of the class. Unlike non-`static` member functions, a `static` member function does not have a `this` pointer, because `static` data members and `static` member functions exist independently of any objects of a class.