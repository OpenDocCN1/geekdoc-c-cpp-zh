```
void f(T i, T* p);
void g(int i) {
f(i,&i); // OK
f(i,"Remember!"); // error,ambiguous: T is int or T is const char?
}
```

# 23.5.2.1 Reference Deduction

It can be useful to have different actions taken for lvalues and rvalues. Consider a class for holding an {integer,pointer} pair:

```
template<typename T>
class Xref {
public:
Xref(int i, T *p) // store a pointer:Xref is the owner
:index{i}, elem{p}, owner{true}
{}
Xref(int i, T& r) // store a pointer to r,owned bysomeone else :index{i}, elem{&r},
owner{false}
{}
Xref(int i, T&& r) // moverinto Xref,Xref is the owner :index{i}, elem{new T{move(r)}},
owner{true}
{}
~Xref()
{
if(owned) delete elem;
}
// ...
private:
int index;
T* elem;
bool owned;
};
```

So:

```
string x {"There and back again"};
Xref<string> r1 {7,"Here"};
Xref<string> r2 {9,x};
Xref<string> r3 {3,new string{"There"}};
```

```
// r1 owns a copyofstr ing{"Here"} // r2 just refers to x
// r3 owns the string{"There"}
```

Here, r1 picks Xref(int,string&&) because x is an rvalue. Similarly, r2 picks Xref(int,string&) because x is an lvalue.

Lvalues and rvalues are distinguished by template argument deduction: an lvalue of type