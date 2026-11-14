
Printing the information on the objects behaves as before. The big difference is getting information on references and pointers to objects: pr->all_info() and pp->all_info(). In this case, the compiler goes through the following steps:

- 1. What is the static type of pr or pp? That is, how is pr or pp declared?
- 2. Is there a function named all_info in that class?
- 3. Can it be accessed? Or is it private?
- 4. Is it a virtual function? Otherwise just call it.
- 5. What is the dynamic type of pr or pp? That is, what is the type of the object referred to by pr or pp?
- 6. Call all_info from that dynamic type.

To realize these dynamic function calls, the compiler maintains Virtual Function Tables (a.k.a. Virtual Method Tables) or Vtables. They contain function pointers through which each virtual method of the actual object is called. The reference pr has the type person& and refers to an object of type student. Through the vtable of pr, the call of all_info() is directed to student::all_info. This indirection over function pointers adds some extra cost to virtual functions which is significant for tiny functions and negligible for sufficiently large functions.

Definition 6-2 (Late Binding and Dynamic Polymorphism). Selecting the executed method during run time is called Late Binding or Dynamic Binding. It also represents Dynamic Polymorphism—as opposed to static polymorphism with templates.

Analogously to the reference pr, the pointer pp points to a student object, and student::all_info is called by late binding for pp->all_info(). We can also introduce a free function spy_on():

```
void spy_on(const person& p)
{
    p.all_info();
}
```

that provides Tom's complete information thanks to late binding even when we pass a reference to the base class.

The benefit of dynamic selection is that the code exists only once in the executable no matter for how many sub-classes of person it is called. Another advantage over function templates is that only the declaration (i.e., the signature) must be visible when the function is called but not necessarily the definition (i.e., the implementation). This not only saves significant compile time but also allows us to hide our clever (or dirty) implementation from users.

The only entity originating from Tom that calls person::all_info() is p. p is an object of type person to which we can copy a student object. But when we copy a derived to a base class, we lose all extra data of the derived class and only the data members of the base class are really copied. Likewise, the virtual function calls perform those of the base class (here person::all_info()). That is, a base class object does not behave differently when it is constructed by copy from a derived class: all the extra members are gone and the vtable does not refer to any method from the derived class.

In the same way, passing arguments by value to a function:

```
void glueless(person p)
{
    p.all_info();
}
```

disables late binding and thus impedes calling virtual functions from derived classes. This is a very frequent (not only) beginners' error in OOP called *Slicing*. Thus, we must obey the following rule:

### Passing Polymorphic Types
Polymorphic types must always be passed by reference or (smart) pointer!

### 6.1.3.1 Explicit Overriding

Another popular trap that even advanced programmers fall into from time to time is a slightly different signature in the overridden method, like this:

```
class person
{
    virtual void all_info() const { ... }
};
```

```
class student
    : public person
{
    virtual void all_info() { ... }
};
```

```
int main()
{
    student tom("Tom Tomson", "Algebra", "Analysis");
    person& pr = tom;
    pr.all_info();
}
```

In this example, person::all_info() is not late bound to person::all_info() because the signatures are different. This difference is admittedly not obvious, starting with the question of what the method's const qualification has to do with the signature at all. We can think of a member function as having an implicit hidden argument referring to the object itself:

```
void person::all_info_impl(const person& me = *this) { ... }
```

Now it becomes clear that the `const` qualifier of the method qualifies this hidden reference in `person::all_info()`. The corresponding hidden reference in `student::all_info()` is not const-qualified and the method is not considered as an override due to the distinct signature. The compiler will not warn us, just taking `student::all_info()` as new overload. And you can believe us that this little nasty mistake can keep you busy for a while, when classes are large and stored in different files.

We can easily protect ourselves against such trouble with the attribute `override` added to C++11:

```
class student
{
  public:
    virtual void all_info() override { ... }
};
```

Here the programmer declares that this function overrides a `virtual` function of the base class (with the exact same signature). If there is no such function, the compiler will complain:

```
...: error: 'all_info' marked 'override' but doesn't override
       any member functions
virtual void all_info() override {
```

```
...: warning: 'student::all_info' hides overloaded virtual fct.
...: note:   hidden overloaded virtual function 'person::all_info'
             declared here: different qualifiers (const vs none)
virtual void all_info() const { ... }
```

Here, we also get the hint from `clang` that the qualifiers are different. Using `override` for non-virtual functions is an error:

```
...: error: only virtual member fct. can be marked 'override'
       void all_info() override {
```

`override` does not add exciting new functionality to our software, but it can save us from tediously searching for slips of the pen (keyboard). It is advisable to use `override` everywhere, unless backward compatibility is needed. The word is quickly typed (especially with auto-completion) and renders our programs more reliable. It also communicates our intentions to other programmers or even ourselves after not having looked at the code for some years.

Another new attribute in C++11 is `final`. It declares that a `virtual` member function cannot be overridden. This allows the compiler to replace certain indirect vtable calls with direct function calls. Unfortunately, we have no experience so far with how much `final` actually accelerates a virtual function. However, we can also use `final` to protect against surprising behavior of function overriding. Even entire classes can be declared `final` to prevent somebody from deriving from them.

Compared to each other, `override` is a statement regarding the super-classes while `final` refers to sub-classes. Both are contextual keywords; i.e., they are only reserved in a certain context: as qualifiers of member functions. Everywhere else the words could be freely used, for instance, as variable names. However, it is advisable to refrain from doing this for the sake of clarity.

### 6.1.3.2 Abstract Classes

So far we have looked only at examples where a virtual function was defined in a base class and then expanded in derived classes. Sometimes we find ourselves in a situation where we have an ensemble of classes with a common function and need a common super-class to select the classes dynamically. For instance, in Section 6.4, we will introduce solvers that provide the same interface: a solve function. To select them at run time, they need to share a super-class with a solve function. However, there is no universal solve algorithm that we can override later. For that purpose, we need a new feature to state: “I have a virtual function in this class without implementation; this will come later in sub-classes.”

### Definition 6-3 (Pure Virtual Function and Abstract Class)
A virtual function is a Pure Virtual Function when it is declared with = 0. A class containing a pure virtual function is called an Abstract Class.

```
=> c++11/oop_abstract.cpp
```

To be more specific, we expand our person example with an abstract super-class creature:

```
class creature
{
    virtual void all_info() const = 0; // pure virtual
};

class person
: public creature
{ ... };

int main ()
{
    creature some_beast; // Error: abstract class
    person mark("Mark Markson");
    mark.all_info();
}
```

The creation of a creature object fails with a message like this:

```
...: error: variable type 'creature' is an abstract class
creature some_beast;
```

```
...: note: unimplemented pure method 'all_info' in 'creature'
virtual void all_info() const = 0;
```

The object mark behaves as before when we override all_info so that person contains no pure virtual functions.
