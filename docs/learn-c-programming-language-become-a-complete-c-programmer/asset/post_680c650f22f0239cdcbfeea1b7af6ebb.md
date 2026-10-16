
Pointers to data members are described in §20.6.2.

## 20.6.2 Pointers to Data Members

Naturally, the notion of pointer to member applies to data members and to member functions with arguments and return types. For example:

```
struct C {
const char* val;
int i;

void print(int x) { cout << val << x << '\n'; } int f1(int);
void f2();
C(const char* v) { val = v; }
};
using Pmfi = void (C::*)(int); // pointer to member function of C taking an int
using Pm = const char* C::*; // pointer to char* data member of C

void f(C& z1, C& z2) {
C* p = &z2;
Pmfi pf = &C::print; Pm pm = &C::val;

z1.print(1);
(z1.*pf)(2);
z1.*pm = "nv1 "; p->*pm = "nv2 "; z2.print(3);
(p->*pf)(4);

pf = &C::f1; // error : return type mismatch
pf = &C::f2; // error :argument type mismatch
pm = &C::i; // error : type mismatch
pm = pf; // error : type mismatch
}
```

The type of a pointer to function is checked just like any other type.

## 20.6.3 Base and Derived Members

A derived class has at least the members that it inherits from its base classes. Often it has more. This implies that we can safely assign a pointer to a member of a base class to a pointer to a member of a derived class, but not the other way around. This property is often called contravariance. For example:

```
class Text : public Std_interface {
public:
void start();
void suspend();
// ...
virtual void print();
private:
vector s;
};
void (Std_interface::* pmi)() = &Text::print; // error
void (Text::*pmt)() = &Std_interface::start; // OK
```

This contravariance rule appears to be the opposite of the rule that says we can assign a pointer to a derived class to a pointer to its base class. In fact, both rules exist to preserve the fundamental guarantee that a pointer may never point to an object that doesn’t at least have the properties that the pointer promises. In this case, Std_interface::* can be applied to any Std_interface, and most such objects presumably are not of type Text. Consequently, they do not have the member Text::print with which we tried to initialize pmi. By refusing the initialization, the compiler saves us from a run-time error.

## Section 20.7 Advice 611

## 20.7 Advice

[1] Avoid type fields; §20.3.1.
[2] Access polymorphic objects through pointers and references; §20.3.2. [3] Use abstract classes to focus design on the provision of clean interfaces; §20.4. [4] Use override to make overriding explicit in large class hierarchies; §20.3.4.1. [5] Use final only sparingly; §20.3.4.2.

[6] Use abstract classes to specify interfaces; §20.4.
[7] Use abstract classes to keep implementation details out of interfaces; §20.4. [8] A class with a virtual function should have a virtual destructor; §20.4. [9] An abstract class typically doesn’t need a constructor; §20.4.

[10] Prefer private members for implementation details; §20.5.
[11] Prefer public members for interfaces; §20.5.
[12] Use protected members only carefully when really needed; §20.5.1.1. [13] Don’t declare data members protected; §20.5.1.1.

This page intentionally left blank

## Class Hierarchies

> *Abstraction is selective ignorance.*  
> — Andrew Koenig

+   - Introduction
+   - Design of Class Hierarchies
+     - Implementation Inheritance; Interface Inheritance; Alternative Implementations; Localizing Object Creation
+   - Multiple Inheritance
+     - Multiple Interfaces; Multiple Implementation Classes; Ambiguity Resolution; Repeated Use of a Base Class; Virtual Base Classes; Replicated vs. Virtual Bases
+   - Advice

## 21.1 Introduction

The primary focus of this chapter is design techniques, rather than language features. The examples are taken from user-interface design, but I avoid the topic of event-driven programming as commonly used for graphical user interface (GUI) systems. A discussion of exactly how an action on the screen is transformed into a call of a member function would add little to the issues of class hierarchy design and has a huge potential for distraction: it is an interesting and important topic in its own right. For an understanding of GUI, have a look at one of the many C++ GUI libraries.

## 21.2 Design of Class Hierarchies

Consider a simple design problem: Provide a way for a program (“an application”) to get an integer value from a user. This can be done in a bewildering number of ways. To insulate our program from this variety, and also to get a chance to explore the possible design choices, let us start by defining our program’s model of this simple input operation.

The idea is to have a class `Ival_box` (“integer value input box”) that knows what range of input values it will accept. A program can ask an `Ival_box` for its value and ask it to prompt the user if necessary. In addition, a program can ask an `Ival_box` if a user changed the value since the program last looked at it:

```
user
(via “system”)
Ival_box:
value application set_value() get_value()
```

Because there are many ways of implementing this basic idea, we must assume that there will be many different kinds of `Ival_box`es, such as sliders, plain boxes in which a user can type a number, dials, and voice interaction.

The general approach is to build a “virtual user-interface system” for the application to use. This system provides some of the services provided by existing user-interface systems. It can be implemented on a wide variety of systems to ensure the portability of application code. Naturally, there are other ways of insulating an application from a user-interface system. I chose this approach because it is general, because it allows me to demonstrate a variety of techniques and design tradeoffs, because those techniques are also the ones used to build “real” user-interface systems, and – most important – because these techniques are applicable to problems far beyond the narrow domain of interface systems.

In addition to ignoring the topic of how to map user actions (events) to library calls, I also ignore the need for locking in a multi-threaded GUI system.

### 21.2.1 Implementation Inheritance

Our first solution is a class hierarchy using implementation inheritance (as is commonly found in older programs).

Class `Ival_box` defines the basic interface to all `Ival_boxes` and specifies a default implementation that more specific kinds of `Ival_boxes` can override with their own versions. In addition, we declare the data needed to implement the basic notion:

```
class Ival_box {
protected:
int val;
int low, high;
bool changed {false}; // changed by user using set_value()
public:
Ival_box(int ll, int hh):val{ll}, low{ll}, high{hh}{ }

virtual int get_value() { changed = false; return val; } virtual void set_value(int i) {
changed = true; val = i; } virtual void reset_value(int i) { changed = false; val = i; }
virtual void prompt() { }
virtual bool was_changed() const { return changed; }

virtual ~Ival_box() { }; };
// for application // for user
// for application

Section 21.2.1 Implementation Inheritance 615
The default implementation of the functions is pretty sloppy and is provided here primarily to illustrate the intended semantics. A realistic class would, for example, provide some range checking. A programmer might use these “ival classes” like this:

```
void interact(Ival_box * pb)
{
pb->prompt(); // alert user
// ...
int i = pb->get_value();

if (pb->was_changed()) {
// ... newvalue; do something ... }
else {
// ... do something else ... }
}

void some_fct() {
unique_ptr<Ival_box> p1 {new Ival_slider{0,5}}; // Ival_slider derived from Ival_box
interact(p1.get());

unique_ptr<Ival_box> p2 {new Ival_dial{1,12}};
interact(p2.get());
}
```

Most application code is written in terms of (pointers to) plain Ival_boxes the way interact() is. That way, the application doesn’t have to know about the potentially large number of variants of the Ival_box concept. The knowledge of such specialized classes is isolated in the relatively few functions that create such objects. This isolates users from changes in the implementations of the derived classes. Most code can be oblivious to the fact that there are different kinds of Ival_boxes.

I use unique_ptr (§5.2.1, §34.3.1) to avoid forgetting to delete the ival_boxes.
To simplify the discussion, I do not address issues of how a program waits for input.
Maybe the program really does wait for the user in get_value() (e.g., using a get() on a future; §5.3.5.1), maybe the program associates the Ival_box with an event and prepares to respond to a callback, or maybe the program spawns a thread for the Ival_box and later inquires about the state of that thread. Such decisions are crucial in the design of user-interface systems. However, discussing them here in any realistic detail would simply distract from the presentation of programming techniques and language facilities. The design techniques described here and the language facilities that support them are not specific to user interfaces. They apply to a far greater range of problems.

The different kinds of Ival_boxes are defined as classes derived from Ival_box. For example:

```
class Ival_slider : public Ival_box {
private:
// ... graphics stuff to define what the slider looks like,etc. ...
public:
Ival_slider(int, int);
int get_value() override; // get value from user and deposit it in val
void prompt() override;
};
```

The data members of Ival_box were declared protected to allow access from derived classes. Thus, Ival_slider::get_value() can deposit a value in Ival_box::val. A protected member is accessible from a class’s own members and from members of derived classes, but not to general users (see §20.5).

In addition to Ival_slider, we would define other variants of the Ival_box concept. These could include Ival_dial, which lets you select a value by turning a knob;
