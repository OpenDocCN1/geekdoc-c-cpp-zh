Cat cat;
Platypus platypus;
p = &AnyMammal;

```
cout << "p is pointing to an object of type \;
cout << typeid("p\).name() << endl;
```

```
p = &cat;
cout << "p is pointing to an object of type \;
cout << typeid("p\).name() << endl;
```

```
p = &platypus;
cout << "p is pointing to an object of type \;
cout << typeid("p\).name() << endl;
```

```
return 0;
}
```

# output
p p is pointing to an object of type Mammal
p p is pointing to an object of type Cat
p p is pointing to an object of type Platypus

Since the base class is polymorphic, p points to the actual object even though it is a pointer to a base class type.

When typeid is applied to a base-class pointer of a polymorphic class, the type of object pointed to is the type of the actual object. When typeid is applied to a pointer of a non-polymorphic class hierarchy, then the type of the object to which the pointer was pointing at the time of its declaration will be returned. For example, comment out the virtual keyword before the function lays_eggs in Mammal and then compile and run the program.

When the pointer being dereferenced is null, typeid will throw a bad_type exception.

# typeid And References

References to an object of a polymorphic class hierarchy work in the same manner as pointers. When typeid is applied to a reference to an object of a polymorphic class, it will return the type of the object actually being referred to, which may be an object of a