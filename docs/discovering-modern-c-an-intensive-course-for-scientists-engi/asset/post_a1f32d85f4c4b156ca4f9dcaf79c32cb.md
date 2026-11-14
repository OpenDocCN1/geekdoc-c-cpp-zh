
- Inheritance means that derived classes contain all data and function members of their base class(es).
- Polymorphism is the ability of an identifier to be interpreted depending on context or parameters. We have seen polymorphism in terms of function overloading and template instantiation. In this chapter, we will see another form that is related to inheritance.
- Late Binding is the selection of the actually called function at run time.

We have already discussed abstraction, encapsulation, and some kinds of polymorphism. In this chapter, we will introduce inheritance and the related polymorphism.

To demonstrate the classical usage of OOP, we will use a simple example that has only a tangential relation to science and engineering but allows us to study the C++ features in a comprehensible fashion. Later, we will provide examples from science and introduce more sophisticated class hierarchies.

## 6.1.1 Base and Derived Classes

```
=> c++03/oop_simple.cpp
```

A use case for all kinds of OOP principles is a database of different types of people. We start with a class that will be the basis of all other classes in this section:

```
class person
{
    public:
    person() {}
    explicit person(const string& name) : name(name) {}
    void set_name(const string& n) { name = n; }
    string get_name() const { return name; }
    void all_info() const
    { cout << "person My name is " << name << endl; }

    private:
    string name;
};
```

For the sake of simplicity, we only use one member variable for the name and refrain from splitting it into first, middle, and last names.

Typical OOP classes often contain getter and setter methods for member variables (which some IDEs insert automatically in the class whenever a new variable is added). Nonetheless, introducing a getter and a setter unconditionally for each member is considered bad practice nowadays because it contradicts the idea of encapsulation. Many even consider this an Anti-Pattern since we are directly reading and writing the internal states to perform tasks with the object. Instead the object should provide methods that perform their respective tasks without uncovering internal states.

The method all_info is intended to be Polymorphic in the sense that it depends on the person's actual class type which information we get about a person.

Our first type of person is student:

```
class student
    : public person
{
    public:
        student(const string& name, const string& passed)
            : person(name), passed(passed) {}

        void all_info() const
        {
            cout << "[student] My name is " << get_name() << endl;
            cout << "I passed " << passed << endl;
        }

    private:
        string passed;
};
```

The class student is Derived from person. As a consequence, it contains all members of person: both methods and data members; that is, it Inherits them from its base (person). Figure 6-1 shows the public and private members (denoted by +/- respectively) of person and student. A student can access them all and a (mere) person only its own. Accordingly, if we added a member to person like a method get_birthday(), it would be added to student as well.

In other words, a student Is-A person. Therefore, student can be used wherever person can: as an argument, in assignments, etc. Just as in real life, if we allow that a person can open a bank account, so can a student (we're sorry for all the hard-up students with different experiences). We will later see how this is expressed in C++.

![](img/ba4defb7bf504868bf19451f3cd4b9bb_314_0.png)

Figure 6-1: Derived class

Regarding the visibility of names, the derived class is similar to an inner scope: in addition to the class's members, we see those of its base class (and their base classes as well). When a derived class contains a variable or function with the same name, those of the base class are hidden, similarly again to a scope. In contrast, we can still access members of the derived class by name qualification like person::all_info. Even a function (overload) with an equal name and a different signature is hidden in the derived class—C++ hides names not signatures. They can be made visible in the derived class with a using declaration like using base::fun. Then those function overloads with a signature different from all overloads in the derived class are accessible without qualification.

When we use our two classes in the following way:

```cpp
person mark("Mark Markson");
mark.all_info();

student tom("Tom Tomson", "Algebra, Analysis");
tom.all_info();
```

```cpp
person p(tom);
person& pr = tom;     // or pr(tom) or pr(tom)
person* pp = &tom;    // or pp(&tom) or pp(tom)

p.all_info();
pr.all_info();
pp->all_info();
```

we might be surprised if not disappointed by the result:

```
[person] My name is Mark Markson
[student] My name is Tom Tomson
I passed the following grades: Algebra, Analysis
[person] My name is Tom Tomson
[person] My name is Tom Tomson
[person] My name is Tom Tomson
```

Only when the variable has type student do we get the grading information. When we try to handle a student as a regular person, the program compiles and runs but we do not see the additional student information.

Nonetheless, we are allowed to

- Copy a student to a person;
- Refer to a student as a person; and
- Pass a student as a person argument to a function.

More formally phrased: a derived class is a Sub-type of its base class, and wherever the base class is required its derived classes are accepted.

A good way to understand sub- and super-types is to think of sub- and super-sets. A class models a certain set, and a sub-set of this set is modeled by a sub-class that constrains the super-class by invariants. Our person class models all kind of people, and we model groups of people with classes that are sub-classes of person.

The paradox of this picture is that the derived classes may contain additional member variables, and the number of possible objects is larger than that of its super-class. This paradox can be resolved by considering appropriate invariants to model the sub-set properly. For instance, the invariant of the student class would be that no two objects with the same name and different grades exist. This would guarantee that the cardinality of the student set is not larger than that of the person set. Unfortunately, the before-mentioned invariant is hard to verify (even for those languages with automatic invariant check) and must be implicitly established by well-designed program logic.

When we derive from a base class, we can specify how restrictive the access to the members inherited from that class is. In the preceding example we derived publicly so that all inherited members have the same accessibility in the base and derived classes. If we derive a class as protected, public base class members are protected in the derived class while the others preserve their accessibility. Members of privately derived classes are all private (this form of inheritance is only used in advanced OOP applications). When we do not specify how the base class is accessed, the derivation is by default private when we define a class and public for a struct.

## 6.1.2 Inheriting Constructors

One method that is not inherited implicitly from the base class is the constructor. Therefore, the following program does not compile:

```
class person
{
public:
    explicit person(const string& name) : name(name) {}
    // ...
};
```

```
class student : public person
{
}; // No constructor for string defined
```

```
int main ()
{
    student tom("Tom Tomsom"); // Error: no string constructor
}
```

The class student inherits all methods from person except the string constructor. C++11 allows us to inherit all constructors from a base class with a using declaration:

```
class student
{
public:
    using person::person;
};
```

When constructors with the same signature exist in both classes, that from the derived class is preferred.

So far, we have applied three of the four before-mentioned basic principles: encapsulation, inheritance, and sub-typing. But there is still something missing and we will introduce it now.

## 6.1.3 Virtual Functions and Polymorphic Classes

The full potential of object-oriented programming is only unleashed with virtual functions. Their presence changes the behavior of a class fundamentally, leading to the following:

> **Definition 6-1 (Polymorphic Types).** Classes containing one or more **virtual** functions are called **_Polymorphic Types_**.

We continue with the preceding implementation and only add the attribute virtual to the method `all_info()`:

```cpp
class person
{
    virtual void all_info() const { cout << "My name is " << name << endl; }
    ...
};
```

```cpp
class student
    : public person
{
    virtual void all_info() const {
        person::all_info(); // call all_info() from person
        cout << "I passed the following grades: " << passed << endl;
    }
    ...
};
```

The double colons `::` that we have seen as namespace qualifications (§3.2) can similarly qualify a class from which we call a method. This requires of course that the method is accessible: we cannot call a private method from another class, not even a base class.

Printing the information with the polymorphic class yields a completely different result all of a sudden:

```
[person] My name is Mark Markson
[student] My name is Tom Tomson
I passed the following grades: Algebra, Analysis
[person] My name is Tom Tomson
[student] My name is Tom Tomson
I passed the following grades: Algebra, Analysis
[student] My name is Tom Tomson
I passed the following grades: Algebra, Analysis
```
