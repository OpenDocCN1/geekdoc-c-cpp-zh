Notice in Main() that we can call Save() from an instance of an employee, but to load a new employee we call DataStorage.Load(). To load an employee, we generally don't already have an employee instance to load into, so an instance method on Employee would be less than ideal. An alternative to calling Load on DataStorage would be to add a static Load() method (see the section Static, later in this chapter) to Employee so that it would be possible to call Employee.Load() (using the Employee class, not an instance of Employee).

Observe the inclusion of the using System.IO directive at the top of the listing. This makes each IO class accessible without prefixing it with the full namespace.

# Access Modifiers

When declaring a field earlier in the chapter, you prefixed the field declaration with the keyword public. public is an access modifier that identifies the level of encapsulation associated with the member it decorates. Five access modifiers are available: public, private, protected, internal, and protected internal. This section considers the first two.

# BEGINNER TOPIC

# Encapsulation Part 2: Information Hiding

Besides wrapping data and methods together into a single unit, encapsulation is also about hiding the internal details of an object's data and behavior. To some degree, methods do this: from outside a method, all that is visible to a caller is the method declaration. None of the internal implementation is visible. Object-oriented programming enables this further, however, by providing facilities for controlling the extent to which members are visible from outside the class. Members that are not visible outside the class are private members.

In object-oriented programming, encapsulation is the term for not only grouping data and behavior, but also hiding data within a class (the capsule) so that minimum access about the inner workings of a class is exposed outside the class. This reduces the chances that callers will modify the data inappropriately.