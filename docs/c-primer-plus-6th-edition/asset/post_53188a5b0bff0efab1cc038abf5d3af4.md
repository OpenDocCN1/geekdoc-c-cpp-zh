
The template aspect means that you have to provide a specific type when declaring an valarray. When declaring an object, you follow the identifier valarray with angle brackets that contain the desired type:

```
valarray<int> q_values; // an array of int
valarray<double> weights; // an array of double
```

You've seen this syntax in Chapter 4, "Compound Types," with the vector and array classes, and it's pretty easy. (Those template classes also can hold numbers, but they don't provide the arithmetic support that the valarray class does.)

The class aspect means that to use valarray objects, you need to know something about class constructors and other methods. Here are several examples that you use some of the constructors:

```
double gpa[5] = {3.1, 3.5, 3.8, 2.9, 3.3};
valarray<double> v1; // an array of double, size 0
valarray<int> v2(8); // an array of 8 elements
valarray<int> v3(10,8); // an array of 8 elements, each set to 10
```

```
valarray<double> v4(gpa,4); // an array of 4 elements
// initialized to the first 4 elements of gpa
```

As you can see, you can create an array of zero size, an empty array of a given size, with all elements initialized to the same value, and an array initialized using the values from an ordinary array. With C++11, you can also use an initializer list:

```
valarray<int> v5 = {20, 32, 17, 9}; // C++11
```

Here are a few of the methods:

- The operator[]() method provides access to individual elements.
- The size() method returns the number of elements.
- The sum() method returns the sum of the elements.
- The max() method returns the largest element.
- The min() method returns the smallest element.

## The Student Class Design

At this point, the design plan for the Student class is to use a string object to represent name and a valarray<double> object to represent the quiz scores. How should this be done? You might be tempted to publicly derive a Student class from these two classes. That would be an example of multiple inheritance, which C++ allows, but it would be inappropriate. The reason is that the relationship of a student to these classes doesn't fit the is-a model. A student is not a name. A student is not an array of quiz scores. What you have is a has-a relationship. A student has a name, and a student has an array of quiz scores. The usual C++ technique for modeling has-a relationships is to use composition or containment—that is, to create a class composed of, or containing, members that are objects of another class. For example, you can begin a Student class declaration like this:

```cpp
class Student
private:
    string name; // use a string object for name
    valarray<double> scores; // use a valarray<double> object for scores
...
};
```

As usual, the class makes the data members private. This implies that the Student class member functions can use the public interfaces of the string and valarray<double> to access and modify the name and scores objects, but the outside world cannot do so. The only access the outside world would have to name and scores is through the public interface defined for the Student class (see Figure 14.1). A common of describing this is to say that the Student acquires the implementation of its member objects doesn't inherit the interface. For example, a Student object uses the string implementation rather than a char* name or a char name implementation for holding the name. But a Student object does not innately have the ability to use the string operator+= a function for appending.

## Interfaces and Implementations

With public inheritance, a class inherits an interface, and, perhaps, an implementation. (Pure virtual functions in a base class can provide an interface without an implementation.) Acquiring the interface is part of the is-a relationship. With composition, on the other hand, a class acquires the implementation without the interface. Not inheriting the interface is part of the has-a relationship.

That a class object automatically acquire the interface of a contained object is a good thing for a has-a relationship. For example, string overloads the + operator to concatenate two strings, conceptually, it doesn't make sense to concatenate two Student objects. One reason is not to use public inheritance in this case. On the other hand, parts of the interface for the contained class may make sense for the new class. For example, you might want to use the operator<() method from the string interface to sort Student objects by name by defining a Student::operator<() member function that internally uses the string::operator<>() function. Let's move on to some details.

## Classes with Object Members

![](img/cd111a87c1db9aff4db4b18834327463_803_0.png)

- access with Student class scope through string class public methods invoked by name object
- access within Student class scope through valarray<double> class methods invoked by scores object

```cpp
class Student
{
private:
    string name;
    valarray<double> scores;
    ...
};
```

Figure 14.1 Objects within objects: containment.

## The Student Class Example

At this point you need to provide the Student class declaration. It should, of course, include constructors and at least a few functions to provide an interface for the Student class. Listing 14.1 defining all the constructors inline. It also supplies some friends for input and output.

Listing 14.1 student.h

```cpp
// student.h -- defining Student class using containment
#ifndef STUDENT_H
#define STUDENT_H

#include <iostream>
#include <string>
#include <valarray>

class Student
{
private:
    typedef valarray<double> ArrayDB;
    string name;            // contained object
    ArrayDB scores;             // contained object
    // private method for scores
    std::ostream & operator<<(std::ostream & os) const;

public:
    Student() : name(""), scores() {}
    explicit Student(const string& s) : name(s), scores() {}
    explicit Student(int n) : name(""), scores(n) {}
    Student(const string& s, int n) : name(s), scores(n) {}
    Student(const string& s, const ArrayDB& a) : name(s), scores(a) {}
    Student(const char* str, const double* pd, int n) : name(str), scores(pd, n) {}

    double Average() const;
    const string& Name() const;
    double& operator[](int i);
    const double operator[](int i) const;

    // friends
    friend std::ostream& operator>>(std::ostream& is, Student& stu);
    friend std::istream& getline(std::ostream& is, Student& stu);
    friend std::ostream& operator<<(std::ostream& os, const Student& stu);
};
```

In order to simplify notation, the Student class contains this typedef: `typedef vector<double> ArrayDB;`. This enables the remaining code to use the more convenient notation ArrayDB instead of vector<double>. Thus, methods and functions can refer to ArrayDB. Placing this typedef in the private portion of the class definition means that it can be used internally but not by outside users of the Student class. Note the use of the keyword explicit: Recall that a constructor that can be called with one argument serves as an implicit conversion function from the argument type to the class type. This is often not a good idea. In the second constructor, for instance, the first argument represents the number of elements in an array rather than a value for the array, so having the constructor serve as int-to-Student conversion function does not make sense. Using explicit turns off implicit conversions. If this keyword was omitted, code like the following would be possible:

```cpp
Student doh("Homer", 10); // store "Homer", create array of 10 elements
doh = 5; // reset name to "", reset to empty array of 5 elements
```

Here, the attentive programmer instead of doh[0]. If the constructor omitted, 5 would be converted to a temporary Student object, using the constructor Student(5), with the value of "" used to set the member name. Then assignment would replace the original doh with the temporary object. With explicit in place, the compiler will catch the assignment operator as an error.

## C++ and Constraints

C++ is full of features that allow programmers to constrain programmatic constructs to certain limits—explicit to remove implicit conversion of single-argument constructors, const to constrain the use of methods to modify data, and more. The underlying motive is simply this: Compile-time errors are better than runtime errors.

## Initializing Contained Objects

Note that constructors use the by-now-familiar member list syntax to initialize the name and scores members. In some cases earlier in the book, such as the following, constructors use this list to initialize members that are built-in types:

```cpp
Queue::Queue(int qs) : qsize(qs) {} // initialize qsize to qs
```

This code uses the name of data (qsize) in a member initializer list. Also constructors from previous examples, such as the following, use a member initializer list to initialize the base-class portion of a derived object:

```cpp
hasDMA::hasDMA(const hasDMA & hs) : baseDMA(hs) {}
```

For inherited objects, constructors use the class name in the member initializer list to invoke a base-class constructor. For member objects, constructors use the member name. For example, look at the constructor in Listing 14.1:

```cpp
Student(const char str, const double* pd, int n)
  : name(str), scores(pd, n) {}
```

Because it inherits member objects, this constructor uses the member names, not the class names, in the initialization list. Each item in this initialization list invokes the matching constructor. That is, name (str) invokes the string (const*) and scores (pd, n) invokes the ArrayDB(const double *, int) constructor, which is of the typedef, really the valarray<double>(const double *, int).

What happens if you don't use the initialization list syntax? As with inherited components, C++ requires that all member objects be constructed before the rest of an object is constructed. If you omit the initialization list, C++ uses the default constructors for the member objects' classes.
