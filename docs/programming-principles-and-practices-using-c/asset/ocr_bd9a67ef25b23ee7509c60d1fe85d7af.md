```
cout << p->value;
if (p=p->succ) cout << ",";
}
cout << "}";
}

print_all(norse_gods);
cout<<"\n";

print_all(greek_gods);
cout<<"\n";
```

This should give

{ Freia, Odin, Thor }
{ Zeus, Poseidon, Ares, Athena, Hera }

# 17.10 The this pointer

Note that each of our list functions takes a **Link** \* as its first argument and accesses data in that object. That’s the kind of function that we often make member functions. Could we simplify **Link** (or link use) by making the operations members? Could we maybe make the pointers private so that only the member functions have access to them? We could:

```
**class** Link {
**public**:
string value;

Link(const string& v, Link* p = **nullptr**, Link* s = **nullptr**)
: value(v), prev(p), succ(s) { }

Link* insert(Link* n); // insert n before this object
Link* add(Link* n); // insert n after this object
Link* erase(); // remove this object from list
Link* find(const string& s); // find s in list
const Link* find(const string& s) const; // find s in const list (see §18.5.1)

Link* advance(int n) const; // move n positions in list

Link* next() const { return succ; }
Link* previous() const { return prev; }
```