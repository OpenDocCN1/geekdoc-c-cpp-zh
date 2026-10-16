
## 26.4 Advice

[1] Let the compiler/implementation generate specializations as needed; §26.2.1. [2] Explicitly instantiate if you need exact control of the instantiation environment; §26.2.2. [3] Explicitly instantiate if you optimize the time needed to generate specializations; §26.2.2. [4] Avoid subtle context dependencies in a template definition; §26.3. [5] Names must be in scope when used in a template definition or findable through argumentdependent lookup (ADL); §26.3, §26.3.5.

[6] Keep the binding context unchanged between instantiation points; §26.3.4. [7] Avoid fully general templates that can be found by ADL; §26.3.6. [8] Use concepts and/or **static_assert** to avoid using inappropriate templates; §26.3.6. [9] Use **using**-declarations to limit the reach of ADL; §26.3.6. [10] Qualify names from a template base class with -> or **T::** as appropriate; §26.3.7.

## Templates and Hierarchies

> *Euclid’s and Beethoven’s Fifth; knowing just one of them marks you as semi-educated.*
> – Stan Kelley-Bootle

- Introduction
- Parameterization and Hierarchy
- Generated Types; Template Conversions
- Hierarchies of Class Templates
- Templates as Interfaces
- Template Parameters as Base Classes
- Composing Data Structures; Linearizing Class Hierarchies
- Advice

## 27.1 Introduction

Templates and derivation are mechanisms for building new types out of existing ones, for specifying interfaces, and generally for writing useful code that exploits various forms of commonality:

- A template class defines an interface. The template’s own implementation and those of its specializations can be accessed through that interface. The source code implementing the template (in the template definition) is identical for all parameter types. The implementations of different specializations can be very different, but they should all implement the semantics specified for the primary template. A specialization can add functionality to what the primary template offers.
- A base class defines an interface. The class’s own implementation and those of its derived classes can (using virtual functions) be accessed through that interface. The implementations of different derived classes can be very different, but they should all implement the semantics specified for the base class. A derived class can add functionality to what the base class offers.

From a design perspective, the two approaches are close enough to deserve a common name. Since both allow an algorithm to be expressed once and applied to a variety of types, people refer to both as *polymorphic* (from Greek “many shapes”). To distinguish them, what virtual functions provide is called *run-time polymorphism*, and what templates offer is called *compile-time polymorphism* or *parametric polymorphism*.

The rough duality of the generic and object-oriented approaches can be deceptive. Object-oriented programmers tend to focus on the design of hierarchies of classes (types) with an interface being an individual class (Chapter 21). Generic programmers tend to focus on the design of algorithms with the concepts for template arguments providing an interface that can accommodate many types (Chapter 24). The ideal for a programmer should be mastery of both techniques to the point where either can be used where most appropriate.

In many cases, the optimal design contains elements of both. For example vector<Shape_*> is a compile-time polymorphic (generic) container holding elements from a run-time polymorphic (object-oriented) hierarchy (§3.2.4).

Generally, good object-oriented programming requires more foresight than good generic programming because all types in a hierarchy must explicitly share an interface defined as a base class. A template will accept any type that meets its concept as an argument, even if there is no explicitly declared commonality among those types. For example accumulate() (§3.4.2, §24.2, §40.6.1) will accept vector of int s and list of complex<double> even though there are no declared relationship between the two element types and no declared relationship between the two sequence types.

## 27.2 Parameterization and Hierarchy

As shown in §4.4.1 and §27.2.2, combinations of templates and class hierarchies are the basis for many useful techniques. So:

- When do we choose to use a class template?
- When do we rely on a class hierarchy?

Consider these questions from a slightly simplified and abstract point of view:

```
template<typename X>
class Ct {
X mem; public:
X f();
int g();
void h(X); };

template<> class Ct<A> {
A *mem; // the representation can differ from that of the primary template public:
A f();
int g();
void h(A);
void k(int); // added functionality
};

// interface expressed in terms of the parameter
// specialization (for A)
```

```
Ct<A> cta; // specialization for A
Ct<B> ctb; // specialization for B
```

Given that, we can use f(), g(), and h() on the variables cta and ctb, using the implementations of Ct<A> and Ct<B>, respectively. I used an explicit specialization (§23.5.3.4) to show that implementations can vary from what the primary template offers and that it is possible to add functionality. The simpler case – without added functionality – is by far the more common.

The rough equivalent using a hierarchy is:

```
class X { // ...
};
```

```
class Cx {
X mem;
public:
virtual X& f();
virtual int g();
virtual void h(X&); };
```

// interface expressed in terms of types in scope

```
Class DA : public Cx { public:
X& f();
int g();
void h(X&);
};
```

// derived class

```
Class DB : public Cx { // derived class
DB *p; // representation can be more extensive than what the base provides public:
X& f();
int g();
void h(X&);
void k(int); // added functionality
};
```

```
Cx& cxa {*new DA}; // cxa is an interface to a DA
```

```
Cx& cxb {*new DB}; // cxb is an interface to a DB
```

Given that, we can use f(), g(), and h() on the variables cxa and cxb, using the implementations of DA and DB, respectively. I use references in the hierarchical version to reflect that we must manipulate derived class objects through pointers or references to preserve run-time polymorphic behavior.

In either case, we manipulate objects that share a common set of operations. From this simplified and abstract point of view we can observe:

- If the types in the interface to the generated or derived classes need to differ, templates have an advantage. To gain access to differing interfaces for derived classes through a base, we must use some form of explicit casting (§22.2).

- If the implementations of generated or derived classes differ only through a parameter or differ only in a few special cases, templates have an advantage. Irregular implementations can be expressed through derived classes or specializations.

- If the actual types of objects used cannot be known at compile time, a class hierarchy is essential.

- If a hierarchical relationship is required between generated or derived types, hierarchies have an advantage. The base class provides a common interface. Conversions among template specializations must be explicitly defined by the programmer (§27.2.2).

- If explicit use of free store (§11.2) is undesirable, templates have an advantage.
- If run-time efficiency is at such a premium that inlining of operations is essential, templates should be used (because effective use of hierarchy requires the use of pointers or references, which inhibit inlining).

Keeping base classes minimal and type-safe can be a struggle. Expressing the interface in terms of existing types that cannot vary for derived classes can be a struggle. Often the result is a compromise that either overconstrains the base class interface (e.g., we pick a class **X** with a “rich interface” which must be implemented by all derived classes and “for all time”) or underconstrains (e.g., we use **void*** or a minimal **Object***).

The combination of templates and class hierarchies provides design choices and flexibility beyond what either can offer by itself. For example, a pointer to a base class can be used as a template argument to provide run-time polymorphism (§3.2.4), and a template parameter can be used to specify a base class interface to provide type safety (§26.3.7, §27.3.1).

It is not possible to have a **virtual** function template (§23.4.6.2).

### 27.2.1 Generated Types

A class template is usefully understood as a specification of how particular types are to be created. In other words, the template implementation is a mechanism that generates types when needed based on a specification. Consequently, a class template is sometimes called a *type generator*.

As far as the C++ language rules are concerned, there is no relationship between two classes generated from a single class template. For example:

```
class Shape {
// ...
};
```

```
class Circle : public Shape { {
// ...
};
```

Given these declarations, people sometimes think that there must be an inheritance relationship between **set<Circle>** and **set<Shape>** or at least between **set<Circle*>** and **set<Shape*>**. This is a serious logical error based on a flawed argument: “A **Circle** is a **Shape**, so a set of **Circle**s is also a set of **Shape**s; therefore, I should be able to use a set of **Circle**s as a set of **Shape**s.” The “therefore” part of this argument doesn’t hold. The reason is that a set of **Circle**s guarantees that the members of the set are **Circle**; a set of **Shape**s does not provide that guarantee. For example:

Section 27.2.1 Generated Types 763

```
class Triangle : public Shape { // ...
};
```

```
void f(set<Shape *>& s) {
```
