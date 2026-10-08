
## TRY THIS

> Before reading further, try to see how many errors you can find in f(). Specifically, which of the calls of poor() could cause the program to crash?

At first glance, the calls look fine, but this is the kind of code that costs a programmer long nights of debugging and gives a quality engineer nightmares.

1.  Passing the wrong element type, e.g., poor(&s0[0], s0.size()). Also, s0 might be empty, in which case &s0[0] is wrong.
2.  Use of a “magic constant” (here, correct): poor(s1, 10). Also, wrong element type.
3.  Use of a “magic constant” (here, incorrect): poor(s2, 20).
4.  Correct (easily verified): first call poor(p1, 1).
5.  Passing a null pointer: second call poor(p1, 1).
6.  May be correct: poor(q, max). We can’t be sure from looking at this code fragment. To see if q points to an array with at least max elements, we have to find the definitions of q and max and determine their values at our point of use.

In each case, the errors are simple. We are not dealing with some subtle algorithmic or data structure problem. The problem is that poor()’s interface, involving an array passed as a pointer, opens the possibility of a collection of problems. You may appreciate how the problems were obscured by our use of “technical” unhelpful names, such as p1 and s0. However, mnemonic, but misleading, names can make such problems even harder to spot.

In theory, a compiler could catch a few of these errors (such as the second call of poor(p1, 1) where p1==0), but realistically we can be saved from disaster for this particular example only because the compiler catches the attempt to define objects of the abstract class Shape. However, that is unrelated to poor()’s interface problems, so we should not take too much comfort from that. In the following, we use a variant of Shape that is not abstract so as not to get distracted from the interface problems.

How come the poor(&s0[0], s0.size()) call is an error? The &s0[0] refers to the first element of an array of Circles; it is a Circle*. We expect a Shape* and we pass a pointer to an object of a class derived from Shape (here, a Circle*). That’s obviously acceptable: we need that conversion so that we can do object-oriented programming, accessing objects of a variety of types through their common interface (here, **Shape** (§14.2). However, **poor()** doesn't just use that **Shape\*** as a pointer; it uses it as an array, subscripting its way through that array:

```cpp
for (int i = 0; i < sz; ++i) p[i].draw();
```

That is, it looks at the objects starting at memory locations &**p[0]**, &**p[1]**, &**p[2]**, etc.:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_978_0.png)

In terms of memory addresses, these pointers are **sizeof(Shape)** apart (§17.3.1). Unfortunately for **poor()**'s caller, **sizeof(Circle)** is larger than **sizeof(Shape)**, so that the memory layout can be visualized like this:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_978_1.png)

That is, **poor()** is calling **draw()** with a pointer into the middle of the **Circles**! This is likely to lead to immediate disaster (crash).

The call **poor(s1,10)** is sneakier. It relies on a “magic constant” so it is immediately suspect as a maintenance hazard, but there is a deeper problem. The only reason the use of an array of **Polygons** doesn't immediately suffer the problem we saw for **Circles** is that a **Polygon** didn't add data members to its base class **Shape** (whereas **Circle** did; see §13.8 and §13.12); that is, **sizeof(Shape)===sizeof(Polygon)** and – more generally – a **Polygon** has the same memory layout as a **Shape**. In other words, we were “just lucky”; a slight change in the definition of **Polygon** will cause a crash. So **poor(s1,10)** works, but it is a bug waiting to happen. This is emphatically not quality code.

What we see here is the implementation reason for the general language rule that “a **D** is a **B**” does not imply “a **Container<D>** is a **Container<B>**” (§19.3.3). For example:

```cpp
class Circle : public Shape { /* ... */ };

void fv(vector<Shape>&);
void f(Shape&);
```

```cpp
void g(vector<Circle>& vd, Circle & d)
{
    f(d);        // OK: implicit conversion from Circle to Shape
    fv(vd);      // error: no conversion from vector<Circle> to vector<Shape>
}
```

OK, so the use of **poor**() is very bad code, but can such code be considered embedded systems code; that is, should this kind of problem concern us in areas where safety or performance matters? Can we dismiss it as a hazard for programmers of non-critical systems and just tell them, “Don’t do that”? Well, many modern embedded systems rely critically on a GUI, which is almost always organized in the object-oriented manner of our example. Examples include the iPod user interface, the interfaces of some cell phones, and operator’s displays on “gadgets” up to and including airplanes. Another example is that controllers of similar gadgets (such as a variety of electric motors) can constitute a classic class hierarchy. In other words, this kind of code – and in particular, this kind of function declaration – is exactly the kind of code we should worry about. We need a safer way of passing information about collections of data without causing other significant problems.

So, we don’t want to pass a built-in array to a function as a pointer plus a size. What do we do instead? The simplest solution is to pass a reference to a container, such as a **vector**. The problems we saw for

```cpp
void poor(Shape* p, int sz);
```

simply cannot occur for

```cpp
void general(vector<Shape>&);
```

If you are programming where `std::vector` (or the equivalent) is acceptable, simply use **vector** (or the equivalent) consistently in interfaces; never pass a built-in array as a pointer plus a size.

If you can’t restrict yourself to **vector** or equivalents, you enter a territory that is more difficult and the solutions there involve techniques and language features that are not simple – even though the use of the class (*Array_ref*) we provide is straightforward.

### 25.4.3 A solution: an interface class

Unfortunately, we cannot use `std::vector` in many embedded systems because it relies on the free store. We can solve that problem either by having a special implementation of **vector** or (more easily) by using a container that behaves like a **vector** but doesn't do memory management. Before outlining such an interface class, let's consider what we want from it:

- It is a reference to objects in memory (it does not own objects, allocate objects, delete objects, etc.).
- It “knows” its size (so that it is potentially range checked).
- It “knows” the exact type of its elements (so that it cannot be the source of type errors).
- It is as cheap to pass (copy) as a (pointer,count) pair.
- It does *not* implicitly convert to a pointer.
- It is easy to express a subrange of the range of elements described by an interface object.
- It is as easy to use as built-in arrays.

We will only be able to approximate “as easy to use as built-in arrays.” We don't want it to be so easy to use that errors start to become likely.
Here is one such class:

```cpp
template<typename T>
class Array_ref {
public:
    Array_ref(T* pp, int s):p(pp), sz(s) { }

    T& operator [](int n) { return p[n]; }
    const T& operator [](int n) const { return p[n]; }

    bool assign(Array_ref a)
    {
        if (a.sz!=sz) return false;
        for (int i=0; i<sz; ++i) { p[i]=a.p[i]; }
        return true;
    }

    void reset(Array_ref a) { reset(a.p, a.sz); }
    void reset(T* pp, int s) { p=pp; sz=s; }

    int size() const { return sz; }

    // default copy operations:
    // Array_ref doesn't own any resources
    // Array_ref has reference semantics
private:
    T* p;
    int sz;
};
```

**Array_ref** is close to minimal:

- No **push_back()** (that would require the free store) and no **at()** (that would require exceptions).
- **Array_ref** is a form of reference, so copying simply copies (**p,sz**).
- By initializing with different arrays, we can have **Array_ref**s that are of the same type but have different sizes.
- By updating (**p,size**) using **reset()**, we can change the size of an existing **Array_ref** (many algorithms require specification of subranges).
- No iterator interface (but that could be easily added if we needed it). In fact, an **Array_ref** is in concept very close to a range described by two iterators.

An **Array_ref** does not own its elements; it does no memory management; it is simply a mechanism for accessing and passing a sequence of elements. In that, it differs from the standard library **array** (§20.9).

To ease the creation of **Array_ref**s, we supply a few useful helper functions:

```cpp
template<typename T> Array_ref<T> make_ref(T* pp, int s)
{
    return (pp)? Array_ref<T>{pp,s} : Array_ref<T>{nullptr,0};
}
```

If we initialize an **Array_ref** with a pointer, we have to explicitly supply a size. That’s an obvious weakness because it provides us with an opportunity to give the wrong size. It also gives us an opportunity to use a pointer that is a result of an implicit conversion of an array of a derived class to a pointer to a base class, such as **Polygon[10]** to **Shape*** (the original horrible problem from §25.4.2), but sometimes we simply have to trust the programmer.

We decided to be careful about null pointers (because they are a common source of problems), and we took a similar precaution for empty **vectors**:

```cpp
template<typename T> Array_ref<T> make_ref(vector<T>&& v)
{
    return (v.size())? Array_ref<T>{&v[0],v.size()} : Array_ref<T>{nullptr,0};
}
```
