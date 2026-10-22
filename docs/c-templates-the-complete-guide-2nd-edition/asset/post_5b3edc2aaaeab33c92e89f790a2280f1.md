
## 18.5 New Forms of Design Patterns

The availability of static polymorphism in C++ leads to new ways of implementing classic design patterns. Take, for example, the Bridge pattern, which plays a major role in many C++ programs. One goal of using the Bridge pattern is to switch between different implementations of an interface.

![](img/0d5072d8203dcaf6ef50e76a3d9a3203_459_0.png)

Figure 18.3. Bridge pattern implemented using inheritance

According to [DesignPatternsGoF], this is usually done using an interface class that embeds a pointer to refer to the actual implementation and delegating all calls through this pointer (see Figure 18.3).

However, if the type of the implementation is known at compile time, we exploit the power of templates instead (see Figure 18.4). This leads to more type safety (in part, by avoiding pointer conversions) and better performance.

![](img/0d5072d8203dcaf6ef50e76a3d9a3203_459_1.png)

Figure 18.4. Bridge pattern implemented using templates

## 18.6 Generic Programming

Static polymorphism leads to the concept of generic programming. However, there is no single agreed-on definition of generic programming (just as there is no single agreed-on definition of object-oriented programming). According to [CzarneckiEiseneckerGenProg], definitions go from programming with generic parameters to finding the most abstract representation of efficient algorithms. The book summarizes: Generic programming is a subdiscipline of computer science that deals with finding abstract representations of efficient algorithms, data structures, and other software concepts, and with their systematic organization.... Generic programming focuses on representing families of domain concepts. (pp. 169-170) In the context of C++, generic programming is sometimes defined as programming with templates (whereas object-oriented programming is thought of as programming with virtual functions). In this sense, just about any use of C++ templates could be thought of as an instance of generic programming. However, practitioners often think of generic programming as having an additional essential ingredient: Templates have to be designed in a framework for the purpose of enabling a multitude of useful combinations.

By far the most significant contribution in this area is the Standard Template Library (STL), which later was adapted and incorporated into the C++ standard library. The STL is a framework that provides a number of useful operations, called algorithms, for a number of linear data structures for collections of objects, called containers. Both algorithms and containers are templates. However, the key is that the algorithms are not member functions of the containers. Instead, the algorithms are written in a generic way so that they can be used by any container (and linear collection of elements). To do this, the designers of STL identified an abstract concept of iterators that can be provided for any kind of linear collection. Essentially, the collection-specific aspects of container operations have been factored out into the iterators’ functionality.

As a consequence, we can implement an operation such as computing the maximum value in a sequence without knowing the details of how values are stored in that sequence:

Click here to view code image

```cpp
template<typename Iterator>
Iterator max_element (Iterator beg, //refers to start of collection
Iterator end) //refers to end of collection
{
// use only certain Iterator operations to traverse all elements
// of the collection to find the element with the maximum value
// and return its position as Iterator
... 
}
```

Instead of providing all useful operations such as max_element() for every linear container, the container has to provide only an iterator type to traverse the sequence of values it contains and member functions to create such iterators:

Click here to view code image

```cpp
namespace std {
template<typename T, ...>
class vector {
public:
using const_iterator = ...; // implementation-specific iterator
... // type for constant vectors
const_iterator begin() const; // iterator for start of collection
const_iterator end() const; // iterator for end of collection
... 
};

template<typename T, ...>
class list {
public:
using const_iterator = ...; // implementation-specific iterator
... // type for constant lists
const_iterator begin() const; // iterator for start of collection
const_iterator end() const; // iterator for end of collection
... 
};
}
```

Now, we can find the maximum of any collection by calling the generic max_element() operation with the beginning and end of the collection as arguments (special handling of empty collections is omitted):

Click here to view code image

```cpp
int main()
{
    std::vector<MyClass> c1;
    std::list<MyClass>   c2;
    ...
    printMax(c1);
    printMax(c2);
}
```

poly/printmax.cpp

```cpp
#include <vector>
#include <list>
#include <algorithm>
#include <iostream>
#include "MyClass.hpp"

template<typename T>
void printMax (T const& coll)
{
  // compute position of maximum value
  auto pos = std::max_element(coll.begin(),coll.end());

  // print value of maximum element of coll (if any):
  if (pos != coll.end()) {
    std::cout << *pos << '\n';
  }
  else {
    std::cout << "empty" << '\n';
  }
}

int main()
{
  std::vector<MyClass> c1;
  std::list<MyClass> c2;
  …
  printMax(c1);
  printMax(c2);
}
```

By parameterizing its operations in terms of these iterators, the STL avoids an explosion in the number of operation definitions. Instead of implementing each operation for every container, we implement the algorithm once so that it can be used for every container. The *generic glue* is the iterators, which are provided by the containers and used by the algorithms. This works because iterators have a certain interface that is provided by the containers and used by the algorithms. This interface is usually called a *concept*, which denotes a set of constraints that a template has to fulfill to fit into this framework. In addition, this concept is open for additional operations and data structures.

You’ll recall that we described a *concepts* language feature earlier in Section 18.4 on page 377 (and in more detail in [Appendix E](#)), and indeed, the language feature maps exactly onto the notion here. In fact, the term *concept* in this context was first introduced by the designers of the STL to formalize their work. Soon thereafter, work commenced to try to make these notions explicit in our templates.

The forthcoming language feature will help us to specify and double check requirements on iterators (since there are different iterator categories, such as *forward* and *bidirectional* iterators, multiple corresponding concepts would be involved; see Section E.3.1 on page 744). In today’s C++, however, the concepts are mostly implicit in the specifications of our generic libraries (and the standard C++ library in particular). Some features and techniques (e.g., `static_assert` and SFINAE) do permit some amount of automated checking, fortunately.

In principle, functionality such as an STL-like approach could be implemented with dynamic polymorphism. In practice, however, it would be of limited use because the iterator concept is too lightweight compared with the virtual function call mechanism. Adding an interface layer based on virtual functions would most likely slow down our operations by an order of magnitude (or more).

Generic programming is practical precisely because it relies on static polymorphism, which resolves interfaces at compile time. On the other hand, the requirement that the interfaces be resolved at compile time also calls for new design principles that differ in many ways from object-oriented design principles. Many of the most important of these *generic design principles* are described in the remainder of this book. Additionally, Appendix E delves deeper into generic programming as a development paradigm by describing direct language support for the notion of concepts.

## 18.7 Afternotes

Container types were a primary motivation for the introduction of templates into the C++ programming language. Prior to templates, polymorphic hierarchies were a popular approach to containers. A popular example was the National Institutes of Health Class Library (NIHCL), which to a large extent translated the container class hierarchy of Smalltalk (see Figure 18.5).
