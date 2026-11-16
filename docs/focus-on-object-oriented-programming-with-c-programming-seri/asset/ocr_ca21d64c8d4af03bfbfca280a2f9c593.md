Here is an example:

```
// Memory leak

bool AdjustTemperature(HTHING hThing) {
    if (!hThing)
        return(false);

    // Instantiate a Thing using a handle
    Thing *pThing = new Thing(hThing);
    if (!pThing)
        return(false);

    // Get Thing's color and adjust temperature accordingly
    switch(pThing->Color()) {
    case BLUE:   AdjustTemperature(5);  return(true);
    case RED:    AdjustTemperature(-5); return(true);
    default:     break;
    }

    // For what colors does this get executed?
    delete pThing;
    return( false );
}
```

As you can see in the above code fragment, the programmer saved a few clock cycles by not using a local Boolean variable to keep track of success or failure. He didn't need a local variable because whenever his code encountered an error it just returned to the caller. This code does return the correct result to its caller. However, if the color of the Thing is red or blue, the memory that pThing points to never gets deleted. Note that if you must implement memory leakage in legacy code, this technique can also be implemented in good old C by using malloc and free instead of new and delete.

# Tactic No. 3: Use Numerous Pointers with the Same Name

C++ allows and encourages a programmer to declare an automatic variable close to the point of usage. So, you can declare an automatic variable that will point to a quantity of allocated memory right at the point of allocation. This capability provides the memory leaker with a unique opportunity. Declare a pointer at the start of a function (in the traditional manner), and declare another pointer of the same name within an inner scope, at the point of instantiation. This will create a fairly confusing memory leak. Here is an example: