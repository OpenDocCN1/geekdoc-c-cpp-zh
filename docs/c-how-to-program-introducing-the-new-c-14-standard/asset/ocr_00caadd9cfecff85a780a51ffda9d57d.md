# Section 9.12 Composition: Objects as Members of Classes

+   - A class can have objects of other classes as members—this concept is called composition.
+   - Member objects are constructed in the order in which they’re declared in the class definition and before their enclosing class objects are constructed.
+   - If a member initializer is not provided for a member object, the member object’s default constructor will be called implicitly.