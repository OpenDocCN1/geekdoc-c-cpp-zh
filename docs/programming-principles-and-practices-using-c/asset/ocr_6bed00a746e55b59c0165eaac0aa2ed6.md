memory is potentially available for other uses; it is "free." We can illustrate that graphically:

![](bbox=[0.31, 0.14, 0.59, 0.35])

The C++ language makes this "free store" (also called the *heap*) available through an operator called **new**. For example:

```
double* p = new double[4];   // allocate 4 doubles on the free store
```

This asks the C++ run-time system to allocate four **doubles** on the free store and return a pointer to the first **double** to us. We use that pointer to initialize our pointer variable **p**. We can represent this graphically:

![](bbox=[0.18, 0.54, 0.73, 0.73])

The **new** operator returns a pointer to the object it creates. If it created several objects (an array), it returns a pointer to the first of those objects. If that object is of type X, the pointer returned by **new** is of type X*. For example:

```
char* q = new double[4];    // error: double* assigned to char*
```

That **new** returns a pointer to a **double** and a **double** isn't a **char**, so we should not (and cannot) assign it to the pointer to **char** variable **q**.