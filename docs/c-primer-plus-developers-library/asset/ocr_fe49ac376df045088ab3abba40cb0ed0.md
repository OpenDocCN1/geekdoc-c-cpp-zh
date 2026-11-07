scores. What you have here is a *has-a* relationship. A student has a name, and a student has an array of quiz scores. The usual C++ teaching for modeling *has-a* relationships is to use composition or containment—that is, to create a class composed of, or containing, members that are objects of another class. For example, you can begin a Student class declaration like this:

```
```cpp
class Student
{
private:
    string name;                 // use a string object for name
    valarray<double> scores;    // use a valarray<double> object for scores
    ...
};
```
```

As usual, the class makes the data members private. This implies that the Student class member functions can use the public interfaces of the string and valarray<double> classes to access and modify the name and scores objects, but the outside world cannot do so. The only access the outside world will have to name and scores is through the public interface defined for the Student class (see Figure 14.1). A common way of describing this is to say that the Student class acquires the implementation of its member objects but doesn’t inherit the interface. For example, a Student object uses the string implementation rather than a char * name or a char name[26] implementation for holding the name. But a Student object does not innately have the ability to use the string operator+=( ) function for appending.

# Interfaces and Implementations

> With public inheritance, a class inherits an interface, and, perhaps, an implementation. (Pure virtual functions in a base class can provide an interface without an implementation.) Acquiring the interface is part of the *is-a* relationship. With composition, on the other hand, a class acquires the implementation without the interface. Not inheriting the interface is part of the *has-a* relationship.

The fact that a class object doesn’t automatically acquire the interface of a contained object is a good thing for a *has-a* relationship. For example, string overloads the + operator to allow concatenating two strings, but, conceptually, it doesn’t make sense to concatenate two Student objects. That’s one reason not to use public inheritance in this case. On the other hand, parts of the interface for the contained class may make sense for the new class. For example, you might want to use the operator<( ) method from the string interface to sort Student objects by name. You can do so by defining a Student::operator<( ) member function that internally uses the string::operator<( ) function. Let’s move on to some details.