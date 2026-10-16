
```
tie(c,ignore,name) = t; // c=299792458; name="Hannibal"
```

The name ignore refers to an object of a type that ignores assignments. Thus, an ignore in a tie() implies that attempts to assign to its tuple position are ignored. An alternative would be: double c = get<0>(t); // c=299792458

```
string name = get<2>(t); // name="Hannibal"
```

Obviously, this would be more interesting if the tuple came from “elsewhere” so that we didn’t trivially know the element values. For example:

```
tuple<int,double,string> compute();
// ...
double c;
string name;
tie(c,ignore,name) = t; // results in c and name
```

## 34.3 Resource Management Pointers

A pointer points to an object (or not). However, a pointer does not indicate who (if anyone) owns the objects. That is, looking just at a pointer, we have no idea who is supposed to delete the object pointed to, or how, or if at all. In <memory>, we find “smart pointers” to express ownership:

- unique_ptr (§34.3.1) to represent exclusive ownership
- shared_ptr (§34.3.2) to represent shared ownership
- weak_ptr (§34.3.3) to break loops in circular shared data structures

These resource handles are introduced in §5.2.1.

### 34.3.1 unique_ptr

The unique_ptr (defined in <memory>) provides a semantics of strict ownership:

- A unique_ptr owns the object to which it holds a pointer. That is, it is the unique_ptr’s obligation to destroy the object pointed to (if any) by its contained pointer.
- A unique_ptr cannot be copied (has no copy constructor or copy assignment). However, it can be moved.
- A unique_ptr stores a pointer and deletes the object pointed to (if any) using the associated deleter (if any) when it is itself destroyed (such as when a thread of control leaves the unique_ptr’s scope; §17.2.2).

The uses of unique_ptr include:

- Providing exception safety for dynamically allocated memory (§5.2.1, §13.3)
- Passing ownership of dynamically allocated memory to a function
- Returning dynamically allocated memory from a function
- Storing pointers in containers

Think of unique_ptr as being represented by a simple pointer (“the contained pointer”) or (if it has a deleter) as a pair of pointers:

```
up1: unique_ptr<T> up2: unique_ptr<T,D>
object object deleter
```

When a unique_ptr is destroyed, its deleter is called to destroy the owned object. The deleter represents what it means to destroy an object. For example:

- A deleter for a local variable should do nothing.
- A deleter for a memory pool should return the object to the memory pool and destroy it or not, depending on how that pool is defined.
- The default (“no deleter”) version of unique_ptr uses delete. It doesn’t even store the default deleter. It can be a specialization or rely on the empty-base optimization (§28.5). This way unique_ptr supports general resource management (§5.2).

```
template<typename T, typename D = default_delete<T>>
class unique_ptr {
public:
using pointer = ptr; // type of the contained pointer;
// ptr is D::pointer if that is defined, otherwise T*
using element_type = T;
using deleter_type = D;
// ...
};
```

The contained pointer is not directly accessible to users.

```
unique_ptr up {}
unique_ptr up {p} unique_ptr up {p,del} unique_ptr up {up2} up.~unique_ptr()
up=up2
unique_ptr<T,D> (§iso.20.7.1.2)
```

cp is the contained pointer

Default constructor: cp=nullptr; constexpr; noexcept
cp=p; use the default deleter; explicit; noexcept
cp=p; del is the deleter; noexcept
Move constructor: cp.p=up2.p; up2.p=nullptr; noexcept Destructor: if cp!=nullptr invoke cp’s deleter
Move assigment: up.reset(up2.cp); up2.cp=nullptr;
up gets up2’s deleter; up’s old object (if any) is deleted; noexcept
up=nullptr up.reset(nullptr) ; that is, delete up’s old object, if any bool b {up};
Conversion to bool: up.cp!=nullptr; explicit
x=*up x=up.cp; for contained non-arrays only
x=up->m x=up.cp->m; for contained non-arrays only
x=up[n] x=up.cp[n]; for contained arrays only
x=up.get() x=up.cp
del=up.get_deleter() del is up’s deleter
p=up.release() p=up.cp; up.cp=nullptr
up.reset(p) If up.cp!=nullptr call deleter for up.cp; up.cp=p
up.reset() up.cp=pionter{} (probably nullptr);
call the deleter for the old value of up.cp

```
```cpp
up.swap(up2) Exchange up and up2’s values; noexcept
up=up2 up.cp=up2.cp
up<up2 up.cp<up2.cp
up!=up2 !(up==up2)
up>up2 up2<up
up<=up2 !(up2>up)
up>=up2 !(up2<up)
swap(up,up2) up.swap(up2)
```
```

Note: **unique_ptr** does not offer a copy constructor or copy assignment. Had it done so, the meaning of “ownership” would have been very hard to define and/or use. If you feel the need for copies, consider using a **shared_ptr** (§34.3.3.2).

It is possible to have a **unique_ptr** for a built-in array. For example:

```
```cpp
unique_ptr<int[]> make_sequence(int n)
{
unique_ptr p {new int[n]}; for (int i=0; i<n; ++i)
p[i]=i;
return p;
}
```
```

This is provided as a specialization:

```
```cpp
template<typename T, typename D>
class unique_ptr<T[],D> { // specialization for arrays (§iso.20.7.1.3)
// the default D=default_delete<T> comes from the general unique_ptr public:
// ... like the unique_ptr for individual objects, but with [] instead of * and -> ...
};
```
```

To avoid slicing (§17.5.1.4), a **Derived[]** is not accepted as an argument to a **unique_ptr<Base[]>** even if **Base** is a public base of **Derived**. For example:

```
```cpp
class Shape {
// …
};

class Circle : public Base { // …
};

unique_ptr<Shape> ps {new Circle[p,20]}; // OK
unique_ptr<Shape[]> pa {new Circle[] {Circle(p,20), Circle(p,40)}}; // error
```
```

How can we best think of a **unique_ptr**? What are the best ways to use a **unique_ptr**? It is called a pointer (**_ptr**) and I pronounce it “unique pointer,” but clearly it is not just an ordinary pointer (or there would be no point in defining it). Consider a simple technical example:

```
```cpp
unique_ptr<int> f(unique_ptr<int> p)
{
++*p;
return p;
}
```
```

sp1: sp2:
use count<sub>objectdeleter</sub>
The *deleter* is what is used to delete the shared object when the use count goes to zero. The default deleter is the usual **delete** (invoke the destructor, if any, and deallocate free store).

For example, consider a **Node** in a general graph used by an algorithm that adds and removes both nodes and connections between nodes (edges). Obviously, to avoid resource leaks, a **Node** must be deleted if and only if no other node refers to it. We could try:

```
struct Node {
vector<Node*> edges;
// ...
};
```

Given that, answering questions such as “How many nodes points to this node?” is very hard and requires much added “housekeeping” code. We could plug in a garbage collector (§34.5), but that could have negative performance implications if the graph was only a small part of a large application data space. Worse, if the container contained non-memory resources, such as thread handles, file handles, locks, etc., even a garbage collector would leak resources.

Instead, we can use a **shared_ptr**:

```
struct Node {
vector<shared_ptr<Node>> edges;
thread worker;
// ...
};
```

Here, **Node**’s destructor (the implicitly generated destructor will do fine) **deletes** its **edges**. That is, the destructor for each **edges[i]** is invoked, and the **Node** pointed to (if any) is deleted if **edges[i]** was the last pointer to it.

Don’t use a **shared_ptr** just to pass a pointer from one owner to another; that’s what **unique_ptr** is for, and **unique_ptr** does it better and more cheaply. If you have been using counted pointers as return values from factory functions (§21.2.4) and the like, consider upgrading to **unique_ptr** rather than **shared_ptr**.

Do not thoughtlessly replace pointers with **shared_ptrs** in an attempt to prevent memory leaks; **shared_ptrs** are not a panacea nor are they without costs:

- A circular linked structure of **shared_ptrs** can cause a resource leak. You need some logical complication to break the circle, for example, use a **weak_ptr** (§34.3.3).
- Objects with shared ownership tend to stay “live” for longer than scoped objects (thus causing higher average resource usage).
- Shared pointers in a multi-threaded environment can be expensive (because of the need to prevent data races on the use count).
- A destructor for a shared object does not execute at a predictable time, so the algorithms/logic for the update of any shared object are easier to get wrong than for an object that’s not shared. For example, which locks are set at the time of the destructor’s
