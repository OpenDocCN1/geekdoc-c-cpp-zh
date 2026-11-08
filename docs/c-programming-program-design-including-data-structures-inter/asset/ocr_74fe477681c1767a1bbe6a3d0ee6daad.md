# EXAMPLE 11-1

Suppose that we have defined a class called `shape`. The following statements specify that the class `circle` is derived from `shape`, and it is a public inheritance.

```
class circle: public shape
{
    .
    .
    .
};
```

On the other hand, consider the following definition of the class `circle`:

```
class circle: private shape
{
    .
    .
    .
};
```

This is a private inheritance. In this definition, the public members of `shape` become private members of the class `circle`. So any object of type `circle` cannot directly access these members. The previous definition of `circle` is equivalent to:

```
class circle: shape
{
    .
    .
    .
};
```

That is, if we do not use either the `memberAccessSpecifier` `public` or `private`, the public members of a base class are inherited as private members.

The following facts about the base and the derived class should be kept in mind.

+   1. The private members of a base class are private to the base class; hence, the members of the derived class cannot directly access them. In other words, when you write the definitions of the member functions of the derived class, you cannot directly access the private members of the base class.
+   
+   2. The public members of a base class can be inherited either as public members or as private members by the derived class. That is, the public members of the base class can become either public or private members of the derived class.
+   
+   3. The derived class can include additional members—data and/or functions.