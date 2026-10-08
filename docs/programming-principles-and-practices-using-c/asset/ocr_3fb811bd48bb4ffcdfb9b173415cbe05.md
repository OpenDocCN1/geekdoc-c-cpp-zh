That's very much like before. As before, we correct our "mistakes." Correct the name of the god of war:

```
```
Link* p = greek_gods->find("Mars");
if (p) p->value = "Ares";
```
```

Move Zeus into his correct Pantheon:

```
```
Link* p2 = norse_gods->find("Zeus");
if (p2) {
  if (p2==norse_gods) norse_gods = p2->next();
  p2->erase();
  greek_gods = greek_gods->insert(p2);
}
```
```

Finally, let's print out those lists:

```
```
void print_all(Link* p)
{
    cout << "{";
    while (p) {
      cout << p->value;
      if (p=p->next()) cout << ", ";
    }
    cout << "}";
}

print_all(norse_gods);
cout<<"\n";

print_all(greek_gods);
cout<<"\n";
```
```

This should again give

```
```
{ Freia, Odin, Thor }
{ Zeus, Poseidon, Ares, Athena, Hera }
```
```

So, which version do you like better: the one where insert(), etc. are member functions or the one where they are freestanding functions? In this case the differences don't matter much, but see $9.7.5.