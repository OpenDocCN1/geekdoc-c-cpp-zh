Because `operator<<()` is a friend function and not part of the class scope, it has to use `Vector::RECT` instead of just `RECT`. But it is in the `VECTOR` namespace, so it doesn’t need to use the fully qualified name of `VECTOR::Vector::RECT`.

The various methods that can set the mode are more careful to accept only `RECT` and `POL` as valid values, so the final `else` in this function should never be reached. Still, it’s often a good idea to check; such a check can help catch an otherwise obscure programming error.

# Multiple Representations and Classes

Quantities that have different, but equivalent, representations are common. For example, you can measure gasoline consumption in miles per gallon, as done in the United States, or in liters per 100 kilometers, as done in Europe. You can represent a number in string form or numeric form, and you can represent intelligence as an IQ or in kiloturkeys.

Classes lend themselves nicely to encompassing different aspects and representations of an entity in a single object. First, you can store multiple representations in one object. Second, you can write the class functions so that assigning values for one representation automatically assigns values for the other representation(s). For example, the `set_polar()` method for the Vector class sets the mag and ang members to the function arguments, but it also sets the x and y members. Or you can store a single representation and use methods to make other representations available. By handling conversions internally, a class can help you think of a quantity in terms of its essential nature rather than in terms of its representation.

# Overloading Arithmetic Operators for the Vector Class

Adding two vectors is very simple when you use x,y coordinates. You just add the two x components to get the x component of the answer and add the two y components to get the y component of the answer. From this description, you might be tempted to use this code:

```
```cpp
Vector Vector::operator+(const Vector & b) const
{
    Vector sum;
    sum.x = x + b.x;
    sum.y = y + b.y;
    return sum;        // incomplete version
}
```
```

And this would be fine if the object stored only the x and y components. Unfortunately, this version of the code fails to set the polar values.You could fix this problem by adding more code:

```
```cpp
Vector Vector::operator+(const Vector & b) const
{
    Vector sum;
    sum.x = x + b.x;
    sum.y = y + b.y;
    sum.set_ang(sum.x, sum.y);
}
```
```