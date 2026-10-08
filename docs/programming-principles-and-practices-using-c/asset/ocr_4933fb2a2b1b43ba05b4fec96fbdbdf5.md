This is a bit verbose, but we don't need to mention **this** to access a member, so we can abbreviate:

```
Link* Link::insert(Link* n)  // insert n before this object; return n
{
    if (n==nullptr) return this;
    if (this==nullptr) return n;
    n->succ = this;   // this object comes after n
    if (prev) prev->succ = n;
    n->prev = prev;   // this object's predecessor becomes n's predecessor
    prev = n;         // n becomes this object's predecessor
    return n;
}
```

In other words, we have been using the **this** pointer – the pointer to the current object – implicitly every time we accessed a member. It is only when we need to refer to the whole object that we need to mention it explicitly.

Note that **this** has a specific meaning; it points to the object for which a member function is called. It does not point to any old object. The compiler ensures that we do not change the value of **this** in a member function. For example:

```
struct S {
    // ... 
    void mutate(S* p)
    {
        this = p;   // error: this is immutable
        // ... 
    }
};
```

# ### 17.10.1 More link use

Having dealt with the implementation issues, we can see how the use now looks:

```
Link* norse_gods = new Link("Thor");
norse_gods = norse_gods->insert(new Link("Odin"));
norse_gods = norse_gods->insert(new Link("Zeus"));
norse_gods = norse_gods->insert(new Link("Freia"));
```

```
Link* greek_gods = new Link("Hera");
greek_gods = greek_gods->insert(new Link("Athena"));
greek_gods = greek_gods->insert(new Link("Mars"));
greek_gods = greek_gods->insert(new Link("Poseidon"));
```