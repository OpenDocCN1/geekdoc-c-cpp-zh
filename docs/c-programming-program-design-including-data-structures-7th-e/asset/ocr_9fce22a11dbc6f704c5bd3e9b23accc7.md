# GENERAL SYNTAX TO OVERLOAD THE ASSIGNMENT OPERATOR = FOR A CLASS

The general syntax to overload the assignment operator = for a class is described next.

**Function Prototype** (to be included in the definition of the class):

```
const className& operator=(const className&);
```

**Function Definition:**

```
const className& className::operator=
                         (const className& rightObject)
{
        //local declaration, if any

        if (this != &rightObject)  //avoid self-assignment
        {
                //algorithm to copy rightObject into this object
        }

        //Return the object assigned.
        return *this;
}
```

In the definition of the function operator=:

+   - There is only one formal parameter.
+   - The formal parameter is usually a const reference to a particular class.
+   - The function return type is a const reference to a particular class.

We now explain why the return type of the function operator= should be a reference of the class type.

Suppose that the assignment operator = is overloaded for the class rectangleType. The statement:

```
myRectangle = yourRectangle;
```

is equivalent to the statement:

```
myRectangle.operator=(yourRectangle);
```

That is, the object yourRectangle becomes the actual parameter to the function:

```
operator=
```

Now consider the statement:

```
myRectangle = yourRectangle = tempRect;
```

Because the associativity of the operator = is from right to left, this statement is equivalent to the statement:

```
myRectangle.operator=(yourRectangle.operator=(tempRect)); //Line A
```