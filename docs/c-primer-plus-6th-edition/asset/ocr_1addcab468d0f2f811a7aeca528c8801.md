# Reusing Code in C++

In this chapter you'll learn about the following:

+   - Has-a relationships
- Classes with member objects (containment)
- The valarray template class
- Private and protected inheritance
- Multiple inheritance
- Virtual base classes
- Creating class templates
- Using class templates
- Template specializations

One of the main goals of C++ is to facilitate the reuse of code. Public inheritance is one mechanism for achieving this goal, but it's not the only one.This chapter investigates other choices. One technique is to use class members that are objects of another class. This is referred to as containment or composition or layering. Another option is to use private or protected inheritance. Private inheritance, and protected inheritance are typically used to implement has-a relationships—that is, relationships for the new class has an object of another class. For example, a Teacher class might have a BluPlayer object. Multiple inheritance lets you create classes that inherit from two or more base classes, combining their functionality.

Chapter 10, "Objects and Classes," introduces function templates. In this chapter we will look at class templates, which provide another way of reusing code. A class template defines a class in generic terms. Then you can use the template to create specific classes defined for specific types. For example, you could define a general stack template and then use the template to create one class that represents a stack of int values and another class that represents a stack of double values.You could even generate a class that represents a stack of stacks.