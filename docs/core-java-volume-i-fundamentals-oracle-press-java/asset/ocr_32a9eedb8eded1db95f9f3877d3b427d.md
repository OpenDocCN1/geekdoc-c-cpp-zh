+   4. Compare the classes of `this` and `otherObject`. If the semantics of `equals` can change in subclasses, use the `getClass` test:

```
if (getClass() != otherObject.getClass()) return false;
ClassName other = (ClassName) otherObject;
```

If the same semantics holds for *all* subclasses, you can use an `instanceof` test:

```
if (!(otherObject instanceof ClassName other)) return false;
```

Note that the `instanceof` test sets `other` to `otherObject` if it succeeds. No cast is necessary.

+   5. Now compare the fields, as required by your notion of equality. Use `==` for primitive type fields, `Objects.equals` for object fields. Return true if all fields match, false otherwise.

```
return field1 == other.field1
    && Objects.equals(field2, other.field2)
    && ...;
```

If you redefine `equals` in a subclass, include a call to `super.equals(other)`.

![](bbox=[0.127, 0.593, 0.181, 0.635])

# TIP:

If you have fields of array type, you can use the static `Arrays.equals` method to check that the corresponding array elements are equal. Use the `Arrays.deepEquals` method for multidimensional arrays.

![](bbox=[0.127, 0.782, 0.181, 0.822])

# CAUTION:

Here is a common mistake when implementing the `equals` method. Can you spot the problem?