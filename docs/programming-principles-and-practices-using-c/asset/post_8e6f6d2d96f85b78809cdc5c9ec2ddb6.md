
### E.3.2 Window::detach()

It. As shown above, `attach()` is trivial; `detach()` is slightly less simple. Looking in `Window.cpp`, we find:

```cpp
void Window::detach(Shape& s)
{
    // guess that the last attached will be first released
    for (vector<Shape*>::size_type i = shapes.size(); i > 0; --i)
        if (shapes[i-1]==&s)
            shapes.erase(shapes.begin()+(i-1));
}
```

The `erase()` member function removes ("erases") a value from a `vector`, decreasing the `vector`'s size by one (§20.7.1).

`Window` is meant to be used as a base class, so it has a `virtual` destructor (§17.5.2).

### E.4 Vector_ref

Basically, `Vector_ref` simulates a `vector` of references. You can initialize it with references or with pointers:

-   If an object is passed to `Vector_ref` as a reference, it is assumed to be owned by the caller who is responsible for its lifetime (e.g., the object is a scoped variable).
-   If an object is passed to `Vector_ref` as a pointer, it is assumed to be allocated by `new` and it is `Vector_ref`'s responsibility to delete it.

An element is stored as a pointer – not as a copy of the object – into the `Vector_ref` and has reference semantics. For example, you can put a `Circle` into a `Vector_ref<Shape>` without suffering slicing.

```cpp
template<class T> class Vector_ref {
    vector<T*> v;
    vector<T*> owned;
public:
    Vector_ref() {}
    Vector_ref(T* a, T* b = 0, T* c = 0, T* d = 0);
    ~Vector_ref() { for (int i=0; i<owned.size(); ++i) delete owned[i]; }

    void push_back(T& s) { v.push_back(&s); }
    void push_back(T* p) { v.push_back(p); owned.push_back(p); }

    T& operator[](int i) { return *v[i]; }
    const T& operator[] (int i) const { return *v[i]; }

    int size() const { return v.size(); }
};
```

`Vector_ref`'s destructor `deletes` every object passed to the `Vector_ref` as a pointer.

### E.5 An example: manipulating Widgets

Here is a complete program. It exercises many of the `Widget/Window` features. It is only minimally commented. Unfortunately, such insufficient commenting is not uncommon. It is an exercise to get this program to run and to explain it.
Basically, when you run it, it appears to define four buttons:

```cpp
#include "../GUI.h"
using namespace Graph_lib;

class W7 : public Window {
    // four ways to make it appear that a button moves around:
    // show/hide, change location, create new one, and attach/detach
public:
    W7(int w, int h, const string& t);

    Button* p1;        // show/hide
    Button* p2;
    bool sh_left;

    Button* mvp;       // move
    bool mv_left;

    Button* cdp;       // create/destroy
    bool cd_left;

    Button* adp1;      // activate/deactivate
    Button* adp2;
    bool ad_left;

    void sh();         // actions
    void mv();
    void cd();
    void ad();

    static void cb_sh(Address, Address addr) // callbacks
       { reference_to<W7>(addr).sh(); }
    static void cb_mv(Address, Address addr)
       { reference_to<W7>(addr).mv(); }
    static void cb_cd(Address, Address addr)
       { reference_to<W7>(addr).cd(); }
    static void cb_ad(Address, Address addr)
       { reference_to<W7>(addr).ad(); }
};
```

However, a `W7` (Window experiment number 7) really has six buttons; it just keeps two hidden:

```cpp
W7::W7(int w, int h, const string& t)
     :Window<w,h,t>,
     sh_left{true}, mv_left{true}, cd_left{true}, ad_left{true}
{
p1 = new Button{Point{100,100},50,20,"show",cb_sh};
p2 = new Button{Point{200,100},50,20,"hide",cb_sh};

mvp = new Button{Point{100,200},50,20,"move",cb_mv};

cdp = new Button{Point{100,300},50,20,"create",cb_cd};

adp1 = new Button{Point{100,400},50,20,"activate",cb_ad};
adp2 = new Button{Point{200,400},80,20,"deactivate",cb_ad};

attach(*p1);
attach(*p2);
attach(*mvp);
attach(*cdp);
p2->hide();
attach(*adp1);
}
```

There are four callbacks. Each makes it appear that the button you press disappears and a new one appears. However, this is achieved in four different ways:

```cpp
void W7::sh() // hide a button, show another
{
if (sh_left) {
p1->hide();
p2->show();
}
else { 
    p1->show();
    p2->hide();
    }
    sh_left=!sh_left;
}
```

```cpp
void W7::mv() // move the button
{
    if(mv_left)
    {
        mvp->move(100,0);
    }
    else
    {
        mvp->move(-100,0);
    }
    mv_left = !mv_left;
}
```

```cpp
void W7::cd() // delete the button and create a new one
{
    cdp->hide();
    delete cdp;
    string lab = "create";
    int x = 100;
    if(cd_left)
    {
        lab = "delete";
        x = 200;
    }
    cdp = new Button(Point(x,300), 50, 20, lab, cb_cd);
    attach(*cdp);
    cd_left = !cd_left;
}
```

```cpp
void W7::ad() // detach the button from the window and attach its replacement
{
    if(ad_left)
    {
        detach(*adp1);
        attach(*adp2);
    }
    else
    {
        detach(*adp2);
        attach(*adp1);
    }
    ad_left = !ad_left;
}

int main()
{
W7 w(400,500,"move");
return gui_main();
}
```

This program demonstrates the fundamental ways of adding and subtracting widgets to/from a window — or just appearing to.

# Glossary

> “Often, a few well-chosen words
are worth a thousand pictures.”
— Anonymous

A *glossary* is a brief explanation of words used in a text. This is a rather short glossary of the terms we thought most essential, especially in the earlier stages of learning programming. The index and the “Terms” sections of the chapters might also help. A more extensive glossary, relating specifically to C++, can be found at www.stroustrup.com/glossary.html, and there is an incredible variety of specialized glossaries (of greatly varying quality) available on the web. Please note that a term can have several related meanings (so we occasionally list some) and that most terms we list have (often weakly) related meanings in other contexts; for example, we don’t define *abstract* as it relates to modern painting, legal practice, or philosophy.

-   **abstract class** a class that cannot be directly used to create objects; often used to define an interface to derived classes. A class is made abstract by having a pure virtual function or a protected constructor.
-   **abstraction** a description of something that selectively and deliberately ignores (hides) details (e.g., implementation details); selective ignorance.
-   **address** a value that allows us to find an object in a computer’s memory.
-   **algorithm** a procedure or formula for solving a problem; a finite series of computational steps to produce a result.
-   **alias** an alternative way of referring to an object; often a name, pointer, or reference.
-   **application** a program or a collection of programs that is considered an entity by its users.
-   **approximation** something (e.g., a value or a design) that is close to the perfect or ideal (value or design). Often an approximation is a result of trade-offs among ideals.
-   **argument** a value passed to a function or a template, in which it is accessed through a parameter.
-   **array** a homogeneous sequence of elements, usually numbered, e.g., [0: max].
-   **assertion** a statement inserted into a program to state (assert) that something must always be true at this point in the program.
-   **base class** a class used as the base of a class hierarchy. Typically a base class has one or more virtual functions.
-   **bit** the basic unit of information in a computer. A bit can have the value 0 or the value 1.
-   **bug** an error in a program.
-   **byte** the basic unit of addressing in most computers. Typically, a byte holds 8 bits.
-   **class** a user-defined type that may contain data members, function members, and member types.
-   **code** a program or a part of a program; ambiguously used for both source code and object code.
-   **compiler** a program that turns source code into object code.
-   **complexity** a hard-to-precisely-define notion or measure of the difficulty of constructing a solution to a problem or of the solution itself. Sometimes complexity is used to (simply) mean an estimate of the number of operations needed to execute an algorithm.
-   **computation** the execution of some code, usually taking some input and producing some output.
-   **concept** (1) a notion, an idea; (2) a set of requirements, usually for a template argument.
-   **concrete class** a class for which objects can be created.
-   **constant** a value that cannot be changed (in a given scope); not mutable.
-   **constructor** an operation that initializes ("constructs") an object. Typically a constructor establishes an invariant and often acquires resources needed for an object to be used (which are then typically released by a destructor).
-   **container** an object that holds elements (other objects).
-   **copy** an operation that makes two objects have values that compare equal. See also move.
-   **correctness** a program or a piece of a program is correct if it meets its specification. Unfortunately, a specification can be incomplete or inconsistent, or can fail to meet users’ reasonable expectations. Thus, to produce acceptable code, we sometimes have to do more than just follow the formal specification.
