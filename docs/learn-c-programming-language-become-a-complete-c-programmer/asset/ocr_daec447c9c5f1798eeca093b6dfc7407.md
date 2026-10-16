```
g(2); // call g(double); g(int) is not in scope // ...
}
void g(int); void g3(int);
int x = ff(a);
```

Here, ff() will call g(double). The definition of g(int) comes too late to be considered – just as if ff() had not been a template or if g had named a variable.

# 26.3.3 Point-of-Instantiation Binding

The context used to determine the meaning of a dependent name (§26.3.1) is determined by the use of a template with a given set of arguments. This is called a point of instantiation for that specialization (§iso.14.6.4.1). Each use of a template for a given set of template arguments defines a point of instantiation. For a function template, that point is in the nearest global or namespace scope enclosing its use, just after the declaration that contains that use. For example:

```
void g(int);
template<typename T> void f(T a)
{
g(a); // g is bound at a point of instantiation
void h(int i) {
extern void g(double);
f(i);
}
// point of declaration for f<int>
```

The point of instantiation for f<int>() is outside h(). This is essential to ensure that the g() called in f() is the global g(int) rather than the local g(double). An unqualified name used in a template definition can never be bound to a local name. Ignoring local names is essential to prevent a lot of nasty macro-like behavior.

To enable recursive calls, the point of declaration for a function template is after the declaration that instantiates it. For example:

```
void g(int);
template<typename T> void f(T a)
{
g(a); // g is bound at a point of instantiation if (i) h(a-1); // h is bound at a point of instantiation }
void h(int i) {
extern void g(double);
f(i);
}
// point of declaration for f<int>
```