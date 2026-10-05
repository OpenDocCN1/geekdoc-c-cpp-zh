# Create a Namespace

To create a namespace we use the namespace keyword. For example:

```
namespace A
{
    int var;
    double d = 1.2;
    int f();
    struct S{...};
    class C{...};
} // Semicolon is required
```

Inside a namespace we can declare the elements we want, such as variables, function declarations and definitions, templates, classes, and objects. A namespace is allowed to be declared in the global namespace or within another namespace, but not within a block (e.g., function). A namespace defines its own scope. The scope of each member extends from the point of its declaration to the end of the namespace. Every name declared within a namespace has the name of the namespace (e.g., A) attached to it. Thus the names we use in a namespace do not conflict with the same names in other namespaces or in the global namespace. That is, if we create the namespace A and the B that both contain a variable named var there will be no name conflict between that, is, between the A::var, B::var, and the global var. This is the main advantage of namespaces to avoid name conflicts. In large projects involving many programmers, it is common practice to separate namespaces so that even if the same names are chosen, they will not cause conflicts.

Inside a namespace we can add new elements the name of the namespace. For example, the following statement extends the scope of the namespace A and adds the declaration of the g() function in the elements of A:

```
namespace A
{
    void g();
}
```

As another example, we can use again the A name and add the definition of f() later on. For example:

```
namespace A
{
    int f()
    {}
}
```

Alternatively, we can define it, as we define a function outside its class:

```
int A::f()
{
    ..
```