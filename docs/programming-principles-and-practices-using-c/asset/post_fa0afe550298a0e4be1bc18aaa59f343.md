
Since `draw_lines()` is the first virtual function, it gets the first slot in the **vtbl**, followed by that of `move()`, the second virtual function. A class can have as many virtual functions as you want it to have; its **vtbl** will be as large as needed (one slot per virtual function). Now when we call `x.draw_lines()`, the compiler generates a call to the function found in the `draw_lines()` slot in the **vtbl** for **x**. Basically, the code just follows the arrows on the diagram. So if **x** is a `Circle`, `Circle::draw_lines()` will be called. If **x** is of a type, say `Open_polyline`, that uses the **vtbl** exactly as `Shape` defined it, `Shape::draw_lines()` will be called. Similarly, `Circle` didn't define its own `move()` so `x.move()` will call `Shape::move()` if **x** is a `Circle`. Basically, code generated for a virtual function call simply finds the **vptr**, uses that to get to the right **vtbl**, and calls the appropriate function there. The cost is about two memory accesses plus the cost of an ordinary function call. This is simple and fast.

`Shape` is an abstract class so you can't actually have an object that's just a `Shape`, but an `Open_polyline` will have exactly the same layout as a “plain shape” since it doesn't add a data member or define a virtual function. There is just one **vtbl** for each class with a virtual function, not one for each object, so the **vtbls** tend not to add significantly to a program's object code size.

Note that we didn't draw any non-virtual functions in this picture. We didn't need to because there is nothing special about the way such functions are called and they don't increase the size of objects of their type.

Defining a function of the same name and type as a virtual function from a base class (such as `Circle::draw_lines()`) so that the function from the derived class is put into the **vtbl** instead of the version from the base is called *overriding*. For example, `Circle::draw_lines()` overrides `Shape::draw_lines()`.

Why are we telling you about **vtbls** and memory layout? Do you need to know about that to use object-oriented programming? No. However, many people strongly prefer to know how things are implemented (we are among those), and when people don't understand something, myths spring up. We have met people who were terrified of virtual functions “because they are expensive.” Why? How expensive? Compared to what? Where would the cost matter? We explain the implementation model for virtual functions so that you won't have such fears. If you need a virtual function call (to select among alternatives at run time), you can't code the functionality to be any faster or to use less memory using other language features. You can see that for yourself.

## 14.3.2 Deriving classes and defining virtual functions

We specify that a class is to be a derived class by mentioning a base after the class name. For example:

```cpp
struct Circle : Shape { /* ... */ };
```

By default, the members of a **struct** are **public** (§9.3), and that will include **public** members of a base. We could equivalently have said

```cpp
class Circle : public Shape { public: /* ... */};
```

These two declarations of **Circle** are completely equivalent, but you can have many long and fruitless discussions with people about which is better. We are of the opinion that time can be spent more productively on other topics.

Beware of forgetting **public** when you need it. For example:

```cpp
class Circle : Shape { public: /* ... */};  // probably a mistake
```

This would make **Shape** a **private** base of **Circle**, making **Shape**'s **public** functions inaccessible for a **Circle**. That’s unlikely to be what you meant. A good compiler will warn about this likely error. There are uses for **private** base classes, but those are beyond the scope of this book.

A virtual function must be declared **virtual** in its class declaration, but if you place the function definition outside the class, the keyword **virtual** is neither required nor allowed out there. For example:

```cpp
struct Shape {
  // ...
  virtual void draw_lines() const;
  virtual void move();
  // ...
};
```

```cpp
virtual void Shape::draw_lines() const { /* ... */}  // error
void Shape::move() { /* ... */}    // OK
```

## 14.3.3  Overriding

When you want to override a virtual function, you must use exactly the same name and type as in the base class. For example:

```cpp
struct Circle : Shape {
  void draw_lines(int) const;  // probably a mistake (int argument?)
  void drawlines() const;      // probably a mistake (misspelled name?)
  void draw_lines();            // probably a mistake (const missing?)
  // ...
};
```

Here, the compiler will see three functions that are independent of `Shape::draw_lines()` (because they have a different name or a different type) and won’t override them. A good compiler will warn about these likely mistakes. There is nothing you can or must say in an overriding function to ensure that it actually overrides a base class function.

The `draw_lines()` example is real and can therefore be hard to follow in all details, so here is a purely technical example that illustrates overriding:

```cpp
struct B {
    virtual void f() const { cout << "B::f"; }
    void g() const { cout << "B::g"; }    // not virtual
};

struct D : B {
    void f() const { cout << "D::f"; }    // overrides B::f
    void g() { cout << "D::g"; }
};

struct DD : D {
    void f() { cout << "DD::f"; }         // doesn’t override D::f (not const)
    void g() const { cout << "DD::g"; }
};
```

Here, we have a small class hierarchy with (just) one virtual function `f()`. We can try using it. In particular, we can try to call `f()` and the non-virtual `g()`, which is a function that doesn’t know what type of object it had to deal with except that it is a `B` (or something derived from `B`):

```cpp
void call(const B& b)
{
    b.f();
    b.g();
}

int main()
{
    B b;
    D d;
    DD dd;
    // a D is a kind of B, so call() can accept a D
    // a DD is a kind of D and a D is a kind of B, so call() can accept a DD
    call(b);
    call(d);
    call(dd);

    b.f();
    b.g();

    d.f();
    d.g();

    dd.f();
    dd.g();
}
```

You'll get

B::f B::g D::f B::g D::f B::g B::f B::g D::f D::g DD::f DD::g

When you understand why, you'll know the mechanics of inheritance and virtual functions.

Obviously, it can be hard to keep track of which derived class functions are meant to override which base class functions. Fortunately, we can get compiler help to check. We can explicitly declare that a function is meant to override. Assuming that the derived class functions were meant to override, we can say so by adding `override` and the example becomes

```cpp
struct B {
    virtual void f() const { cout << "B::f "; }
    void g() const { cout << "B::g "; } // not virtual
};
```

```cpp
struct D : B {
    void f() const override { cout << "D::f "; } // overrides B::f
    void g() override { cout << "D::g "; } // error: no virtual B::g to override
};
```

```cpp
struct DD : D {
    void f() override { cout << "DD::f "; } // error: doesn't override
                                             // D::f (not const)
    void g() const override { cout << "DD::g "; } // error: no virtual D::g
                                                    // to override
};
```

Explicit use of **override** is particularly useful in large, complicated class hierarchies.

## 14.3.4 Access

C++ provides a simple model of access to members of a class. A member of a class can be

- *Private:* If a member is **private**, its name can be used only by members of the class in which it is declared.
- *Protected:* If a member is **protected**, its name can be used only by members of the class in which it is declared and members of classes derived from that.
- *Public:* If a member is **public**, its name can be used by all functions.

Or graphically:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_543_0.png)

A base can also be **private**, **protected**, or **public**:

- If a base of class **D** is **private**, its **public** and **protected** member names can be used only by members of **D**.
- If a base of class **D** is **protected**, its **public** and **protected** member names can be used only by members of **D** and members of classes derived from **D**.
- If a base is **public**, its public member names can be used by all functions.

These definitions ignore the concept of “friend” and a few minor details, which are beyond the scope of this book. If you want to become a language lawyer you need to study Sroustrup, *The Design and Evolution of C++* and *The C++ Programing Language*, and the ISO C++ standard. We don’t recommend becoming a language lawyer (someone knowing every little detail of the language definition); being a programmer (a software developer, an engineer, a user, whatever you prefer to call someone who actually uses the language) is much more fun and typically much more useful to society.
