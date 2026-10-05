```
int *p;
try {
    // allocate memory for an int
    p = new int;
}
catch (bad_alloc& xa) {
    cout << "Allocation Failure\n";n    return 1;
}

*p = 100;

cout << "At memory location " << p << endl;
cout << "the value is " << *p << "\n";

delete p;
return 0;

```

This example uses a try...catch exception block that we will discuss subsequently.

The delete operator must only be used with a valid pointer previously returned by new. Using any other type of pointer with delete is undefined and will almost certainly cause serious problems such as a system crash.

Although new and delete perform functions similar to malloc() and free(), they have several advantages. Firstly, new automatically allocates enough memory to hold an object of the specified type. We do not need to use the sizeof operator to get the size of the object. Since the size is computed automatically, it eliminates any possibility of an error in this regard. Second, new automatically returns a pointer to the specified type. We do not need to use an explicit type cast as we do when allocating memory with malloc. Finally, both new and delete can be overloaded, allowing us to create customized allocation systems.