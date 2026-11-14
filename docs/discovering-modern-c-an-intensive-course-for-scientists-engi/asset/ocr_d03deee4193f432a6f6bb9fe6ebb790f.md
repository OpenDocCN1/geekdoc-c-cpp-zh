```
class person { ... };
.
class student
: public virtual person
{
... };
.
class mathematician
: public virtual person
{ ... };
.
```

```
class math_student
: public student, public mathematician
{
public:
math_student(const string& name, const string& passed, const string&
proved) : student(name, passed), mathematician(name, proved) {}
...
};
```

and get the following output that might surprise some of us:

```
[student] My name is
I passed the following grades: Algebra
I proved: Fermat's Last Theorem
```

We lost the value of name despite both student and mathematician calling the person constructor which initializes name. To understand this behavior, we need to know how C++ handles virtual base classes. We know that it is a derived class's responsibility to call the base-class constructor (or else the compiler will generate a call to the default constructor). However, we have only one copy of the person base class. Figure 6-4 illustrates the new memory layout: mathematician and student do not contain the person data any longer but only refer to a common object that is part of the most derived class: math_student.

When creating a student object, its constructor must call the person constructor. And likewise when we create a mathematician object, its constructor will call the person constructor. Now we create a math_student object. The math_student constructor must call the constructors of both mathematician and student. But we know that those constructors should both call the person constructor and thus the shared person part would be constructed twice.

To prevent that, it has been defined that in the case of virtual base classes, it is the responsibility of the Most Derived Class (in our case: math_student) to call the shared base-class constructor (in our case: person). In return, the person constructor calls from mathematician and student are disabled when they are indirectly called from a derived class.

```
-> c++11/oop_mult4.cpp
```

With this in mind, we modify our constructors accordingly: .

```
class student
: public virtual person
{
protected:
student(const string& passed) : passed(passed) {}
```