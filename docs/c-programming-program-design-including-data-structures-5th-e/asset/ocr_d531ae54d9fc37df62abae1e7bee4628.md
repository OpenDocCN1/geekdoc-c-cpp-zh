Clearly, we must first execute the expression:

```
yourRectangle.operator=(tempRect)
```

that is, the expression:

```
yourRectangle = tempRect
```

The value returned by the expression:

```
yourRectangle.operator=(tempRect)
```

will become the parameter to the function operator= in order to assign a value to the object myRectangle (see the statement in Line A). Because the formal parameter of the function operator= is a reference parameter, the expression:

```
yourRectangle.operator=(tempRect)
```

must return a reference to the object, rather than its value. That is, it must return a reference to the object yourRectangle, not the value of yourRectangle. For this reason, the return type of the function to overload the assignment operator = for a class must be a reference to the class type.

Now consider the statement:

```
myRectangle = myRectangle;                         //Line B
```

Here, we are trying to copy the value of myRectangle into myRectangle; that is, this statement is a self-assignment. One reason why we must prevent such assignments is because they waste computer time. First, however, we explain how the body of the assignment operator prevents such assignments.

As noted above, the body of the function operator= does prevent assignments, such as the one given in Line B. Let us see how.

Consider the if statement in the body of the operator function operator=:

```
if (this != &rightObject)  //avoid self-assignment
{
    //algorithm to copy rightObject into this object
}
```

The statement:

```
myRectangle = myRectangle;
```

is compiled into the statement:

```
myRectangle.operator=(myRectangle);
```

Because the function operator= is invoked by the object myRectangle, the pointer this in the body of the function operator= refers to the object myRectangle. Furthermore, because myRectangle is also a parameter of the function operator=,