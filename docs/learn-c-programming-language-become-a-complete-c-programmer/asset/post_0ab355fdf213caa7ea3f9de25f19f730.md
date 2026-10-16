
3. Note that `template<class T>` and `template<typename T>` are synonymous; §23.2.
4. When defining a template, first design and debug a non-template version; later generalize by adding parameters; §23.2.1.
5. Templates are type-safe, but checking happens too late; §23.3.
6. When designing a template, carefully consider the concepts (requirements) assumed for its template arguments; §23.3.
7. If a class template should be copyable, give it a non-template copy constructor and a non-template copy assignment; §23.4.6.1.
8. If a class template should be movable, give it a non-template move constructor and a non-template move assignment; §23.4.6.1.
9. A virtual function member cannot be a template member function; §23.4.6.2.
10. Define a type as a member of a template only if it depends on all the class template’s arguments; §23.4.6.3.
11. Use function templates to deduce class template argument types; §23.5.1.
12. Overload function templates to get the same semantics for a variety of argument types; §23.5.3.
13. Use argument substitution failure to provide just the right set of functions for a program; §23.5.3.2.
14. Use template aliases to simplify notation and hide implementation details; §23.6.
15. There is no separate compilation of templates: `#include` template definitions in every translation unit uses them; §23.7.
16. Use ordinary functions as interfaces to code that cannot deal with templates; §23.7.1.
17. Separately compile large templates and templates with nontrivial context dependencies; §23.7.

- Introduction
- Algorithms and Lifting
- Concepts
  - Discovering a Concept; Concepts and Constraints
- Making Concepts Concrete
  - Axioms; Multi-argument Concepts; Value Concepts; Constraints Checks; Template Definition Checking
- Advice

## Generic Programming

> Now is a good time to put your work on a firm theoretical basis.
> – Sam Morgan

### 24.1 Introduction

What are templates for? In other words, what programming techniques are effective when you use templates? Templates offer:

- The ability to pass types (as well as values and templates) as arguments without loss of information. This implies excellent opportunities for inlining, of which current implementations take great advantage.
- Delayed type checking (done at instantiation time). This implies opportunities to weave together information from different contexts.
- The ability to pass constant values as arguments. This implies the ability to do compile-time computation.

In other words, templates provide a powerful mechanism for compile-time computation and type manipulation that can lead to very compact and efficient code. Remember that types (classes) can contain both code and values.

The first and most common use of templates is to support generic programming, that is, programming focused on the design, implementation, and use of general algorithms. Here, “general” means that an algorithm can be designed to accept a wide variety of types as long as they meet the algorithm’s requirements on its arguments. The template is C++’s main support for generic programming. Templates provide (compile-time) parametric polymorphism.

There are many definitions of “generic programming.” Thus, the term can be confusing. However, in the context of C++, “generic programming” implies an emphasis on the design of general algorithms implemented using templates.

Focusing more on generative techniques (seeing templates as type and function generators) and relying on type functions to express compile-time computation are called template metaprogramming, which is the subject of Chapter 28.

The type checking provided for templates checks the use of arguments in the template definition rather than against an explicit interface (in a template declaration). This provides a compile-time variant of what is often called duck typing (“If it walks like a duck and it quacks like a duck, it’s a duck”). Or – using more technical terminology – we operate on values, and the presence and meaning of an operation depend solely on its operand values. This differs from the alternative view that objects have types, which determine the presence and meaning of operations. Values “live” in objects. This is the way objects (e.g., variables) work in C++, and only values that meet an object’s requirements can be put into it. What is done at compile time using templates does not

Obviously, this computes the sum of the **doubles** in the argument array. Also consider:

```cpp
struct Node {
Node* next;
int data;
};

int sum_elements(Node * first, Node* last) // another concrete algorithm on list of ints
{
int s = 0;
while (first!=last) {
s += first->data;
first = first->next;
}
return s;
}
```

This computes the sum of the **ints** in the singly-linked list implemented by the **Nodes**.

These two code fragments differ in detail and in style, but an experienced programmer will immediately say, “Well, this is just two implementations of the accumulate algorithm.” This is a popular algorithm. Like most popular algorithms, it has many names, including reduce, fold, sum, and aggregate. However, let us try to develop a general algorithm from the two concrete examples in stages, so as to get a feel for the process of lifting. First we try to abstract away the data types so that we don’t have to be specific about

- **double** vs. **int**, or
- array vs. linked list.

To do so, I write some pseudo code:

```text
// pseudo code:

T sum(data)
// somehow parameterize by the value type and the container type
{
T s=0
while (not at end) {
s = s + current value
get next data element
}
return s
}
```

To make this concrete, we need three operations to access the “container” data structure:

- Not at end
- Get current value
- Get next data element

For the actual data, we also need three operations:

- Initialize to zero
- Add
- Return the result

Obviously, this is rather imprecise, but we can turn it into code:

```cpp
// concrete STL-like code:

template<typename Iter, typename Val> Val sum(Iter first, Iter last)
{
  Val s = 0;
  while (first!=last) {
    s=s + *first;
    ++first;
  }
  return s;
}
```

Here, I took advantage of knowing the usual STL way of representing a sequence of values (§4.5). The sequence is represented as a pair of iterators supporting three operations:

- `*` for accessing the current value
- `++` for moving forward to the next element
- `!=` for comparing iterators to check if we are at the end of a sequence

We now have an algorithm (a function template) that can be used for both arrays and linked lists and for both ints and doubles. The array example works immediately because double* is an example of an iterator:

```cpp
double ad[] = {1,2,3,4};
double s = sum<double*>(ad,ad+4);
```

To use the handcrafted singly-linked list, we need to provide an iterator for it. Given a few operations, a Node* can be the iterator:

```cpp
struct Node { Node* next; int data; };

Node * operator++(Node * p) { return p->next; } int operator*(Node * p) { return p->data; } Node* end(lst) { return nullptr; }

void test(Node* lst)
{
  int s = sum<int*>(lst,end(lst));
}
```

I use the nullptr as the end iterator. I use an explicit template argument (here, `<int>`) to allow a caller to specify the type to use for the accumulator variable.

What we have so far is more general than a lot of real-world code. For example, sum() would work for lists of floating-point numbers (of all precisions), for arrays of integers (of all ranges), and for many other types, such as a vector<char>. Importantly, sum() is as efficient as the handcrafted functions we started from. We do not want to achieve generality at the cost of performance.

The experienced programmer will note that sum() can be generalized further. In particular, the use of an extra template argument is awkward, and we required the initial value 0. We can solve that by letting the caller supply an initial value and then deduce Val:

```cpp
template<typename Iter, typename Val> Val accumulate(Iter first, Iter last, Val s) {
while ( first!=last) { s=s+ *first; ++first;
}
return s;
}
```

```cpp
double ad[] = {1,2,3,4};
double s1 = accumulate(ad,ad+4,0.0); double s2 = accumulate(ad,ad+4,0);
```

// accumulate in a double // accumulate in an int

But why +? We sometimes want to multiply elements. In fact, there seem to be quite a few operations we might want to apply to the elements of a sequence. This leads to a further generalization:

```cpp
template<typename Iter, typename Val, typename Oper>
Val accumulate(Iter first, Iter last, Val s, Oper op)
{
while ( first!=last) { s = op(s,*first); ++first;
}
return s;
}
```

We now use the argument op to combine element values with the accumulator. For example:

```cpp
double ad[] = {1,2,3,4};
double s1 = accumulate(ad,ad+4,0.0,std::plus<double>); // as before
double s2 = accumulate(ad,ad+4,1.0,std::multiplies<double>);
```

The standard library provides common operations, such as plus and multiply, as function objects to be used as arguments. Here, we see the utility of having the caller supply the initial value: 0 and * don’t go well together for accumulation. The standard library offers a further generalization of accumulate() that allows a user to provide an alternative to = for combining the result of the “addition” and the accumulator (§40.6).

Lifting is a skill that requires knowledge of an application domain and some experience. The most important single guide for designing algorithms is to lift them from concrete examples without adding features (notation or run-time cost) that would impair their use. The standard-library algorithms are the results of lifting done with great attention to performance issues.

### 24.3 Concepts
