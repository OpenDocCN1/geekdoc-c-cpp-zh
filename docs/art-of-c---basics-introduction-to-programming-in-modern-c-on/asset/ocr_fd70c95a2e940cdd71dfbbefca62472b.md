```
public ref decimal GetCurrentPrice() {}
```

+   * Between the `return` token and the variable returned in a `return` statement in the method. For example:

```
return ref DecimalArray[0];
```

In order for the caller to modify the object's state, the reference return value must be stored to a variable that is explicitly defined as a `ref local`.

The called method may also declare the return value as `ref readonly` to return the value by reference, and enforce that the calling code cannot modify the returned value. The calling method can avoid copying the returned value by storing the value in a local `ref readonly` variable.

# Ref locals

A ref local variable is used to refer to values returned using `return ref`. A ref local variable cannot be initialized to a non-ref return value. In other words, the right-hand side of the initialization must be a reference. Any modifications to the value of the ref local are reflected in the state of the object whose method returned the value by reference.

You define a ref local by using the `ref` keyword before the variable declaration, as well as immediately before the call to the method that returns the value by reference.

For example, the following statement defines a ref local value that is returned by a method named `GetEstimatedValue`:

```
ref decimal estValue = ref Building.GetEstimatedValue();
```