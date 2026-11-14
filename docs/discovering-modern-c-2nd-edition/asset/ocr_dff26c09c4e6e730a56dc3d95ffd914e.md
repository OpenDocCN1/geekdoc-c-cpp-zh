```
void h(A** a) { /* ... */ }
```

An object of type B can be passed to all three functions:

```
B b;
f(b); // Slices!
g(b);
h(&b);
```

In all three cases, the object b is implicitly converted to an object of type A. However, function f is not polymorphic because it slices object b (cf. §6.1.3). Up-casting only fails when the base class is ambiguous. In the current example, we cannot up-cast from D to A:

```
D d;
A ad(d); // Error: ambiguous
```

because the compiler does not know whether the base class A from B or from C is meant. We can clarify this situation with an explicit intermediate up-cast:

```
A ad(B(d));
```

Or we can share A between B and C with virtual bases:

```
struct B : virtual A { ... };
struct C : virtual A {};
```

Now, the members of A exist only once in D. This is usually the best solution for multiple inheritance because we save memory and do not risk inconsistent replication of A.

# 6.5.1.2 Casting Down

Down-casting is the conversion of a pointer/reference to a sub-type pointer/reference. When the actually referred-to object is not of that sub-type, the behavior is undefined. Therefore, we should either test whether the down-cast is correct or ascertain it by the program logic. Recall that we passed an object of type B to a reference and a pointer of type A and respectively A*:

```
void g(A& a) { ... }
void h(A** a) { ... }
```