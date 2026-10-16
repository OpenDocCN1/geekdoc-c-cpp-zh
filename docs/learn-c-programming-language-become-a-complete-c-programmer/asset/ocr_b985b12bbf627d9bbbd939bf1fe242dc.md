+   - If explicit use of free store (§11.2) is undesirable, templates have an advantage.
+   - If run-time efficiency is at such a premium that inlining of operations is essential, templates should be used (because effective use of hierarchy requires the use of pointers or references, which inhibit inlining).

Keeping base classes minimal and type-safe can be a struggle. Expressing the interface in terms of existing types that cannot vary for derived classes can be a struggle. Often the result is a compromise that either overconstrains the base class interface (e.g., we pick a class **X** with a “rich interface” which must be implemented by all derived classes and “for all time”) or underconstrains (e.g., we use **void*** or a minimal **Object***).

The combination of templates and class hierarchies provides design choices and flexibility beyond what either can offer by itself. For example, a pointer to a base class can be used as a template argument to provide run-time polymorphism (§3.2.4), and a template parameter can be used to specify a base class interface to provide type safety (§26.3.7, §27.3.1).

It is not possible to have a **virtual** function template (§23.4.6.2).

# 27.2.1 Generated Types

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