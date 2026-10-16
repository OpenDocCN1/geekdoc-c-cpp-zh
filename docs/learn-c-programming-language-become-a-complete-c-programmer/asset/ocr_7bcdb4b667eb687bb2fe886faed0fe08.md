```
void resize(size_type, T = {}); // change the number of elements void clear() { resize(0); } // makethe vector empty void push_back(const T&); // add an element at the end // ...};
```

```
template<class T, class A>
void vector<T,A>::destroy_elements() {
for (T * p = vb.elem; p!=vb.space; ++p)
p->~T(); // destroyelement (§17.2.4)
vb.space=vb.elem;
}
```

The vector destructor explicitly invokes the T destructor for every element. This implies that if an element destructor throws an exception, the vector destruction fails. This can be a disaster if it happens during stack unwinding caused by an exception and terminate() is called (§13.5.2.5). In the case of normal destruction, throwing an exception from a destructor typically leads to resource leaks and unpredictable behavior of code relying on reasonable behavior of objects. There is no really good way to protect against exceptions thrown from destructors, so the library makes no guarantees if an element destructor throws (§13.2).

Now the constructor can be simply defined:

```
template<class T, class A>
vector<T,A>::vector(size_type n, const T& val, const A& a)
:vb{a,n} // allocate space for n elements {
uninitialized_fill(vb.elem,vb.elem+n,val); // makencopies of val
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
vector<T,A>::vector(vector&& a) // moveconstructor
:vb{move(a.vb)} // transfer ownership
```