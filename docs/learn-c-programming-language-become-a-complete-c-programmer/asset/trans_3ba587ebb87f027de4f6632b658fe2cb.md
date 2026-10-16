

```
void resize(size_type, T = {}); // change the number of elements
void clear() { resize(0); } // make the vector empty
void push_back(const T&); // add an element at the end
// ...};
```

```
template<class T, class A>
void vector<T,A>::destroy_elements() {
for (T * p = vb.elem; p!=vb.space; ++p)
p->~T(); // destroy element (§17.2.4)
vb.space=vb.elem;
}
```

The vector destructor explicitly invokes the T destructor for every element. This implies that if an element destructor throws an exception, the vector destruction fails. This can be a disaster if it happens during stack unwinding caused by an exception and terminate() is called (§13.5.2.5). In the case of normal destruction, throwing an exception from a destructor typically leads to resource leaks and unpredictable behavior of code relying on reasonable behavior of objects. There is no really good way to protect against exceptions thrown from destructors, so the library makes no guarantees if an element destructor throws (§13.2).

Now the constructor can be simply defined:

```
template<class T, class A>
vector<T,A>::vector(size_type n, const T& val, const A& a)
:vb{a,n} // allocate space for n elements {
uninitialized_fill(vb.elem,vb.elem+n,val); // make n copies of val
}
```

The simplification achieved for this constructor carries over to every vector operation that deals with initialization or allocation. For example, the copy constructor differs mostly by using uninitialized_copy() instead of uninitialized_fill():

```
template<class T, class A>
vector<T,A>::vector(const vector<T,A>& a)
:vb{a.alloc,a.size()}
{
uninitialized_copy(a.begin(),a.end(),vb.elem);
}
```

This style of constructor relies on the fundamental language rule that when an exception is thrown from a constructor, subobjects (including bases) that have already been completely constructed will be properly destroyed (§13.3). The uninitialized_fill() algorithm and its cousins (§13.6.1) provide the equivalent guarantee for partially constructed sequences.

The move operations are even simpler:

```
template<class T, class A>
vector<T,A>::vector(vector&& a) // move constructor
:vb{move(a.vb)} // transfer ownership
```
```
```cpp
{
}
```
```

The **vector_base** move constructor will set the argument’s representation to “empty.” For the move assignment, we must take care of the old value of the target:

```
```cpp
template<class T, class A>
vector<T,A>& vector<T,A>::operator=(vector&& a) // move assignment
{

clear(); // destroy elements
swap(*this,a); // transfer ownership

}
```
```

The **clear()** is strictly speaking redundant because I could assume that the rvalue **a** would be destroyed immediately after the assignment. However, I don’t know if some programmer has been playing games with **std::move()**.

## 13.6.3 Assignment

As usual, assignment differs from construction in that an old value must be taken care of. First consider a straightforward implementation:

```
```cpp
template<class T, class A>
vector<T,A>& vector<T,A>::operator=(const vector& a) // offers the strong guarantee (§13.2) {

vector_base<T,A> b(alloc,a.size()); // get memory
uninitialized_copy(a.begin(),a.end(),b.elem); // copy elements
destroy_elements(); // destroy old elements
swap(vb,b); // transfer ownership
return *this; // implicitly destroy the old value

}
```
```

This **vector** assignment provides the strong guarantee, but it repeats a lot of code from constructors and destructors. We can avoid repetition:

```
```cpp
template<class T, class A>
vector<T,A>& vector<T,A>::operator=(const vector& a) // offers the strong guarantee (§13.2) {

vector temp {a}; // copy allocator
std::swap(*this,temp); // swap representations
return *this;

}
```
```

The old elements are destroyed by **temp**’s destructor, and the memory used to hold them is deallocated by **temp**’s **vector_base**’s destructor.

The reason that the standard-library **swap()** (§35.5.2) works for **vector_bases** is that we defined **vector_base** move operations for **swap()** to use.
The performance of the two versions ought to be equivalent. Essentially, they are just two

different ways of specifying the same set of operations. However, the second implementation is shorter and doesn’t replicate code from related vector functions, so writing the assignment that way ought to be less error-prone and lead to simpler maintenance.
Note that I did not test for self-assignment, such as v=v. This implementation of = works by first constructing a copy and then swapping representations. This obviously handles self-assignment correctly. I decided that the efficiency gained from the test in the rare case of self-assignment was more than offset by its cost in the common case where a different vector is assigned.

In either case, two potentially significant optimizations are missing:
- If the capacity of the vector assigned to is large enough to hold the assigned vector, we don’t need to allocate new memory.
- An element assignment may be more efficient than an element destruction followed by an element construction.
Implementing these optimizations, we get:

```
template<class T, class A>
vector<T,A>& vector<T,A>::operator=(const vector& a) // optimized, basic guarantee (§13.2) only {
if (capacity() < a.size()) { // allocate new
vector representation: vector temp {a}; // copy
allocator
swap(*this,temp); // swap representations
return *this; // implicitly destroy the old value
}
```

### Section 13.6.3 Assignment 383

```
if (this == &a) return *this; // optimize self assignment
size_type sz = size();
size_type asz = a.size();
vb.alloc = a.vb.alloc;
if (asz<=sz) {
copy(a.begin(),a.begin()+asz,vb.elem); for (T* p = vb.elem+asz; p!=vb.space; ++p) p ->~T();
} else {
copy(a.begin(),a.begin()+sz,vb.elem); // copy the allocator
// destroy sur plus elements (§16.2.6)
uninitialized_copy(a.begin()+sz,a.end(),vb.space); // construct extra elements }
vb.space = vb.elem+asz;
return *this;
}
```

These optimizations are not free. Obviously, the complexity of the code is far higher. Here, I also test for self-assignment. However, I do so mostly to show how it is done because here it is only an optimization.

The copy() algorithm (§32.5.1) does not offer the strong exception-safety guarantee. Thus,

if `T::operator=()` throws an exception during `copy()`, the `vector` being assigned to need not be a copy of the `vector` being assigned, and it need not be unchanged. For example, the first five elements might be copies of elements of the assigned `vector` and the rest unchanged. It is also plausible that an element — the element that was being copied when `T::operator=()` threw an exception — ends up with a value that is neither the old value nor a copy of the corresponding element in the `vector` being assigned. However, if `T::operator=()` leaves its operands in valid states before it throws (as it should), the `vector` is still in a valid state — even if it wasn’t the state we would have preferred.

The standard-library `vector` assignment offers the (weaker) basic exception-safety guarantee of this last implementation — and its potential performance advantages. If you need an assignment that leaves the `vector` unchanged if an exception is thrown, you must either use a library implementation that provides the strong guarantee or provide your own assignment operation. For example:

```
```cpp
template<class T, class A>
void safe_assign(vector<T,A>& a, const vector<T,A>& b) // simple a = b
{
    vector<T,A> temp{b}; // copy the elements of b into a temporary
    swap(a,temp);
}
```
```

Alternatively, we could simply use call-by-value (§12.2):

```
```cpp
template<class T, class A>
void safe_assign(vector<T,A>& a, vector<T,A> b) // simple a = b (note: b is passed by value) {
    swap(a,b);
}
```
```

I never can decide if this last version is simply beautiful or too clever for real (maintainable) code.

## 13.6.4 Changing Size

One of the most useful aspects of `vector` is that we can change its size to suit our needs. The most popular functions for changing size are `v.push_back(x)`, which adds an `x` at the end of `v`, and `v.resize(s)`, which makes `s` the number of elements in `v`.

### 13.6.4.1 `reserve()`

The key to a simple implementation of such functions is `reserve()`, which adds free space at the end for the `vector` to grow into. In other words, `reserve()` increases the `capacity()` of a `vector`. If the new allocation is larger than the old, `reserve()` needs to allocate new memory and move the elements into it. We could try the trick from the unoptimized assignment (§13.6.3):

```
```cpp
template<class T, class A>
```
```

