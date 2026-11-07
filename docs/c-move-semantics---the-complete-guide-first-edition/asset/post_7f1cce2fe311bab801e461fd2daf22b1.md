
The function `measure()` returns the duration of num iterations performing the three initializations above with strings of a significant length.

Now we combine the different definitions of the class Person above with the measuring function in programs with `main()` functions that call the measurements and print the resulting durations. For example:

```cpp
basics/initclassperson.cpp

#include "initclass.hpp"
#include "initmeasure.hpp"
#include <iostream>
#include <cstdlib>   // for std::atoi

int main(int argc, const char** argv)
{
    int num = 1000;   // num iterations to measure
    if (argc > 1) {
        num = std::atoi(argv[1]);
    }

    // a few iterations to avoid measuring initial behavior:
    measure(5);

    // measure (in integral nano- and floating-point milliseconds):
    std::chrono::nanoseconds nsDur{measure(num)};
    std::chrono::duration<double, std::milli> msDur{nsDur};

    // print result:
    std::cout << num << " iterations take:  "
              << msDur.count() << "ms\n";
    std::cout << "3 inits take on average:  "
              << nsDur.count() / num << "ns\n";
}
```

The other two programs, `basics/initlvalueperf.cpp` and `basics/initmoveperf.cpp`, just use different header files for the other declarations of the class Person.

The effect of running this code on three different platforms with three different compilers with significant optimization activated are as follows:

- In general, the initializations using the classic lvalue references (`const &`) take significantly more time than the other initializations. I have seen factors of up to 2.
- There is no big difference between implementing all nine constructors and just the constructor taking the argument by value and move. Sometimes one approach was a little faster, sometimes the other; often there was no significant difference.

If we benefit from the *small string optimization (SSO)*, by using quite short strings, which means that we do not allocate any memory at all (and move semantics should be no significant help), the numbers are quite close. Nevertheless, you can still measure a slight drawback using the traditional constructor that takes a const lvalue reference. However, this definitely requires that good optimization is activated.

Besides trying the different test programs, you can use basics/initperf.cpp as one combined program that performs all these different measurements on your favorite platform.

However, you might have very expensive members that do not benefit from move semantics (such as an array of 10000 double values):

```cpp
class Person {
private:
    std::string name;
    std::array<double, 10000> values;   // move can't optimize here
public:
    ...
};
```

In such a situation, we get a problem with the approach of taking an initial argument of 10000 doubles by value and move. We have to copy the argument twice, which takes almost twice as much time. See basics/initbigperf.cpp for a complete example program to measure this.

### 4.3.5 Summary for Member Initialization

As a summary, to initialize members for which move semantics makes a significant difference (strings, containers, or classes/arrays with such members), you should use move semantics on one of the following alternatives:

- switch from taking the parameter by lvalue reference to taking it by value and move it into the member
- Overload the constructors for move semantics

The first option allows us to have only one constructor so that the code is easier to maintain. However, this does result in more move operations than necessary. Therefore, if move operations might take significant time, you are better to use multiple overloads.

For example, if we have a class with a string and a vector of values, taking by value and move is usually the right approach:

```cpp
class Person {
private:
    std::string name;
    std::vector<std::string> values;
public:
    Person(std::string n, std::vector<std::string> v)
        : name{std::move(n)}, values{std::move(v)} {
    }
    ...
};
```

However, if we have a std::array member, it is better to overload because moving a std::array still takes significant time even if the members are moved.

```cpp
class Person {
private:
  std::string name;
  std::array<std::string, 1000> values;
public:
  Person(std::string n, const std::array<std::string, 1000>& v)
    : name{std::move(n)}, values{v} {
  }
  Person(std::string n, std::array<std::string, 1000>&& v)
    : name{std::move(n)}, values{std::move(v)} {
  }
  …
};
```

### 4.3.6 Should We Now Always Pass by Value and Move?

The discussion above leads to the question of whether we should now always take arguments by value and move them to set an internal value or member. The answer is **no**.

The special case discussed here is that we *create and initialize* a new value. In this case, this strategy pays off. If we already have a value, which we update or modify, using this approach would be counterproductive.

A simple example would be setters. Consider the following implementation of the class `Person`:

```cpp
class Person {
private:
  std::string first;  // first name
  std::string last;   // last name
public:
  Person(std::string f, std::string l)
    : first{std::move(f)}, last{std::move(l)} {
  }
  …
  void setFirstname(std::string s) {             // take by value
    first = std::move(s);                        // and move
  }
  …
};
```

Assume we use the class as follows:

```cpp
Person p{"Ben", "Cook"};
std::string name1{"Ann"};
std::string name2{"Constantin Alexander"};

p.setFirstname(name1);
p.setFirstname(name2);
p.setFirstname(name1);
p.setFirstname(name2);
```

Each time we set a new firstname we create a new temporary parameter s which allocates its own memory, which is then moved to the value of the member. Thus, we have four allocations (provided we do not have SSO).

Now consider that we implement the setter in the traditional way taking a const lvalue reference:

```cpp
class Person {
private:
    std::string first;   // first name
    std::string last;    // last name
public:
    Person(std::string f, std::string l)
      : first{std::move(f)}, last{std::move(l)} {
    }
    ...
    void setFirstname(const std::string& s) {    // take by reference
        first = s;                               // and assign
    }
    ...
};
```

Binding s to the passed argument will not create a new string. Furthermore, the assignment operator will only allocate new memory if the new length exceeds the current amount of memory allocated for the value. This means that, because we already have a value, the approach of taking the argument by value and move might be counterproductive.

You might wonder whether to overload the setter so that we can benefit from move semantics if the new length exceeds the existing length:

```cpp
class Person {
private:
    std::string first;   // first name
    std::string last;    // last name
public:
    Person(std::string f, std::string l)
      : first{std::move(f)}, last{std::move(l)} {
    }
    ...
    void setFirstname(const std::string& s) {    // take by lvalue reference
        first = s;                               // and assign
    }
    void setFirstname(std::string&& s) {         // take by rvalue reference
        first = std::move(s);                    // and move assign
    }
    ...
};
```

However, even this approach might be counterproductive, because a move assignment might shrink the capacity of first:

```cpp
Person p{"Ben", "Cook"};

p.setFirstname("Constantin Alexander");    // would allocate enough memory
p.setFirstname("Ann");                     // would reduce capacity
p.setFirstname("Constantin Alexander");    // would have to allocate again
```

Even with move semantics, the best approach for setting existing values is to take the new values by const lvalue reference and assign without using std::move().

Taking a parameter by value and moving it to where the new value is needed is only useful when we store the passed value somewhere as a new value (so that we need new memory for it anyway). When modifying an existing value, this policy might be counterproductive.

However, initializing members is not the only application of “take by value and move.” A (member) function adding a new value to a container would be another application:

```cpp
class Person {
private:
    std::string name;
    std::vector<std::string> values;
public:
    Person(std::string n, std::vector<std::string> v)
      : name{std::move(n)}, values{std::move(v)} {
    }
    // better pass by value and move to create a new element:
    void addValue(std::string s)       // take by value
    {
        values.push_back(std::move(s));        // and move into the collection
    }
    ...
};
```

## 4.4 Move Semantics in Class Hierarchies

As we have seen, any declaration of a copy constructor, copy assignment, or destructor disables the automatic support for move semantics. This also applies to polymorphic base classes. However, there are a few additional aspects to consider.

### 4.4.1 Implementing a Polymorphic Base Class

A polymorphic base class usually introduces the virtual member functions you can call for all objects of derived classes. For example:

```cpp
class GeoObj {
public:
    virtual void draw() const = 0;      // pure virtual function (introducing the API)
    ...
    virtual ~GeoObj() = default;        // let delete call the right destructor
```
