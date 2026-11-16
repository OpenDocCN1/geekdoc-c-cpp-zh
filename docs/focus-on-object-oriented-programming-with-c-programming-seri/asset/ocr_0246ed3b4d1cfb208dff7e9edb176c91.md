```
int main() {
    Derived1 dv1;
    Derived2 dv2;
    Base *bptr;

    bptr = &dv1;
    bptr->show();

    bptr = &dv2;
    bptr->show();
    return 0;
}
```

The output generated is now:

```
Derived1
Derived2
```

Now the member functions of the derived classes and not the `Base` class are executed. So the function call:

```
bptr->show();
```

executes different functions depending on the contents of the pointer itself. Once again, the rule is that the function called is based on the contents of the pointer rather than on the type of the pointer, as before.

# Pure Virtual Functions

In our previous example, `Base::show()` is never executed. This is a common situation. There is often no need for the base class version of a particular function. We only use the versions of the function in the derived classes. When this is true, the body of the virtual function in the base class can be removed and the notation `=0` added to the function declaration: