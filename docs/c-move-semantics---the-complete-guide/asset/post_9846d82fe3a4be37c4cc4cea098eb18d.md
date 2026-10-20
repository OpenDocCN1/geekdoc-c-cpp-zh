
## Chapter 4: How to Benefit From Move Semantics

```cpp
GeoObj(std::string n)
  : name{std::move(n)} {
}
public:
  virtual void draw() const = 0;      // pure virtual function (introducing the API)
  ...
  virtual ~GeoObj() = default;        // would disable move semantics for name
protected:
  // enable copy and move semantics (callable only for derived classes):
  GeoObj(const GeoObj&) = default;
  GeoObj(GeoObj&&) = default;
  // disable assignment operator (due to the problem of slicing):
  GeoObj& operator= (GeoObj&&) = delete;
  GeoObj& operator= (const GeoObj&) = delete;
};
```

See *poly/geoobj.hpp* for the complete header file.

### 4.4.2 Implementing a Polymorphic Derived Class

A polymorphic derived class might look as follows (see *poly/polygon.hpp* for the complete header file):[^1]

```cpp
class Polygon : public GeoObj {
  protected:
    std::vector<Coord> points;
  public:
    Polygon(std::string s, std::initializer_list<Coord> = {});  // constructor
    virtual void draw() const override;    // implementation of draw()
};
```

Usually, in a polymorphic derived class there is no need to declare a special member function. Especially, there is no need to declare a virtual destructor again (unless you have to implement it). Declaring a destructor again (whether or not it is virtual) would disable automatic support of move semantics for the members of the derived class (here, for the vector points):

```cpp
class Polygon : public GeoObj {
  protected:
    std::vector<Coord> points;
  public:
    Polygon(std::string s, std::initializer_list<Coord> = {});  // constructor
    ...
    virtual ~Polygon() = default;  // OOPS: don't do that because it disables move semantics
};
```

However, without declaring the destructor, move semantics works for both Polygon members, name and points. Consider the following program:

```cpp
#include "geoobj.hpp"
#include "polygon.hpp"

int main()
{
    Polygon p0{"Poly1", {Coord{1,1}, Coord{1,9}, Coord{9,9}, Coord{9,1}}};
    Polygon p1{p0}; // copy
    Polygon p2{std::move(p0)}; // move

    p0.draw();
    p1.draw();
    p2.draw();
}
```

This program has the following output:

```
polygon '' over
polygon 'Poly1' over (1,1) (1,9) (9,9) (9,1)
polygon 'Poly1' over (1,1) (1,9) (9,9) (9,1)
```

For both members, name and points, the values were moved from p0 to p2.

Note that if you have to implement the move constructor in class Polygon, you need special care to provide the right noexcept condition.

### 4.5 Summary

- Avoid objects with names.
- Avoid unnecessary std::move(). Especially do not use it when returning a local object.
- Constructors that initialize members from parameters, for which move operations are cheap, should take the argument by value and move it to the member.
- Constructors that initialize members from parameters, for which move operations are a significant amount of time, should be overloaded for move semantics for best performance.
- In general, creating and initializing new values from parameters, for which move operations are cheap, should take the arguments by value and move. However, do not take by value and move to update/modify existing values.
- Do not declare a virtual destructor in derived classes (unless you have to implement it).

## Chapter 5: Overloading on Reference Qualifiers

This chapter discusses overloading member functions for different reference qualifiers. As we will see, this will answer the common community question about whether getters should return by value or by constant reference.

### 5.1  Return Type of Getters

When implementing getters for members that are expensive to copy, before C++11 we had the following alternatives:

- Return by value
- Return by const reference

Let us discuss these alternatives briefly.

#### 5.1.1  Return by Value

A getter returning by value would look like this (remember: do not return by value using const otherwise you disable move semantics):

```cpp
class Person
{
private:
    std::string name;
public:
    ...
    std::string getName() const {
        return name;
    }
};
```

This code is safe, but each time we ask for the name, we might copy the name.

For example, just checking whether we have a person with an empty name would have significant overhead:

```cpp
std::vector<Person> coll;
...
for (const auto& person : coll) {
    if (person.getName().empty()) {    // OOPS: copies the name
        std::cout << "found empty name\n";
    }
}
```

If you compare this approach with an approach that returns a reference, you can see that the version that returns the string by value has a performance overhead of a factor between 2 and 100 (provided the names have a significant length so that SSO does not help). Giving access to a member that is an image or a collection of thousands of elements might be even worse. In that case, getters often return by (const) reference to improve the performance.

#### 5.1.2  Return by Reference

A getter returning by reference would look as follows:

```cpp
class Person
{
    private:
        std::string name;
    public:
        ...
        const std::string& getName() const {
            return name;
        }
};
```

This is faster but somewhat unsafe because the caller has to ensure that the object the returned reference refers to lives long enough. In fact, there is a lifetime risk that you use the return value of the getter longer than the object you call the getter for.

One way of falling into this trap is to use the range-based for loop as follows:

```cpp
for (char c : returnPersonByValue().getName()) {  // OOPS: undefined behavior
    if (c == ' ') {
        ...
    }
}
```

Note that on the right side in the header of the loop there is a function that returns a temporary object that we refer to with our getter. However, the range-based for loop is defined so that the code above is equivalent to the following:

```cpp
reference range = returnPersonByValue().getName();
// OOPS: returned temporary object destroyed here
for (auto pos = range.begin(), end = range.end(); pos != end; ++pos) {
    char c = *pos;
    if (c == ' ') {
        ...
    }
}
```

Before we start to iterate, we initialize a reference because we have to use the passed range twice (once to call begin() and once to call end() for it) and want to avoid creating a copy of the range (which might be expensive or even not possible). In general, references extend the lifetime of what they refer to. However, in this case, range does not refer to the Person returned by returnPersonByValue(); range refers to the return value of getName(), which is a reference to a member of a returned Person. Thus, range extends the lifetime of the reference but not of the temporary object that the reference refers to. Therefore, with the end of the first statement, the returned temporary object is destroyed and we use a reference to the name of a destroyed object when we iterate over the characters of the name.

At best, we get a core dump here so that we see that something went significantly wrong. At worst, we get fatal undefined behavior once we ship the software.

Code like this would not be a problem if the getter were to return the name by value. In that case, range would extend the lifetime of a copy of the name so that we can use the name until the end of the lifetime of range.

#### 5.1.3  Using Move Semantics to Solve the Dilemma

With move semantics, we now have a way to solve the dilemma. We can return by reference if it is safe to do so and return by value if we might run into lifetime issues.

The way to program this is as follows:

```cpp
class Person
{
private:
    std::string name;
public:
    std::string getName() && {  // when we no longer need the value
        return std::move(name);  // we steal and return by value
    }
    const std::string& getName() const& {  // in all other cases
        return name;            // we give access to the member
    }
};
```

We overload the getter with different reference qualifiers in the same way as when overloading a function for `&&` and `const&` parameters:

- The version with the `&&` qualifier is used when we have an object where we no longer need the value (an object that is about to die or that we have marked with `std::move()`).

[^1]: *virtual* is not necessary if member functions are declared with *override*. However, I prefer to have it again for better alignment and the rule that either all or no member functions should be *virtual*.
