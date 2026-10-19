Cross-Reference For more suggestions about how to preserve code quality as code is modified, see Chapter 24, “Refactoring.”

# Beware of erosion of the interface’s abstraction under modification

As a class is modified and extended, you often discover additional functionality that’s needed, that doesn’t quite fit with the original class interface, but that seems too hard to implement any other way. For example, in the Employee class, you might find that the class evolves to look like this:

![](bbox=[0.11, 0.22, 0.2, 0.28])

```
C++ Example of a Class Interface That’s Eroding Under Maintenance
class Employee {
public:
    ...
    // public routines
    FullName GetName() const;
    Address GetAddress() const;
    PhoneNumber GetWorkPhone() const;
    ...
    bool IsJobClassificationValid( JobClassification jobClass );
    bool IsZipCodeValid( Address address );
    bool IsPhoneNumberValid( PhoneNumber phoneNumber );
    
    SqlQuery GetQueryToCreateNewEmployee() const;
    SqlQuery GetQueryToModifyEmployee() const;
    SqlQuery GetQueryToRetrieveEmployee() const;
    ...
private:
    ...
};
```

What started out as a clean abstraction in an earlier code sample has evolved into a hodgepodge of functions that are only loosely related. There’s no logical connection between employees and routines that check ZIP Codes, phone numbers, or job classifications. The routines that expose SQL query details are at a much lower level of abstraction than the Employee class, and they break the Employee abstraction.

# Don’t add public members that are inconsistent with the interface abstraction

Each time you add a routine to a class interface, ask “Is this routine consistent with the abstraction provided by the existing interface?” If not, find a different way to make the modification and preserve the integrity of the abstraction.

# Consider abstraction and cohesion together

The ideas of abstraction and cohesion are closely related—a class interface that presents a good abstraction usually has strong cohesion. Classes with strong cohesion tend to present good abstractions, although that relationship is not as strong.

I have found that focusing on the abstraction presented by the class interface tends to provide more insight into class design than focusing on class cohesion. If you see that a class has weak cohesion and aren’t sure how to correct it, ask yourself whether the class presents a consistent abstraction instead.