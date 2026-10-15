# Chapter 9 Inheritance

# 9.1 Creating Subclasses

SR 9.1 A child class is derived from a parent class using inheritance. The methods and variables of the parent class automatically become a part of the child class, subject to the rules of the visibility modifiers used to declare them.

SR 9.2 Because a new class can be derived from an existing class, the characteristics of the parent class can be reused without the error-prone process of copying and modifying code.

SR 9.3 Each inheritance derivation should represent an is-a relationship: the child is-a more specific version of the parent. If this relationship does not hold, then inheritance is being used improperly.

SR 9.4 The protected modifier establishes a visibility level (like public and private) that takes inheritance into account. A variable or method declared with protected visibility can be referenced by name in the derived class, while retaining some level of encapsulation. Protected visibility allows access from any class in the same package.

SR 9.5 The super reference can be used to call the parent’s constructor, which cannot be invoked directly by name. It can also be used to invoke the parent’s version of an overridden method.

```
SR 9.6 public class SchoolBook2 extends Book2
{
    private int ageLevel;

    //-----------------------------------------
    // Constructor: Sets up the schoolbook with the
    // specified number of pages and age level (assumed
    // to be between 4 and 16 inclusive).
    //-----------------------------------------
    public SchoolBook2 (int numPages, int age)
    {
        super(numPages);
        ageLevel = age;
    }

    //-----------------------------------------
    // Returns a string that describes the age level.
    //-----------------------------------------
    public String level ()
    {
        if (ageLevel <= 6)
            return "Pre-school";
```