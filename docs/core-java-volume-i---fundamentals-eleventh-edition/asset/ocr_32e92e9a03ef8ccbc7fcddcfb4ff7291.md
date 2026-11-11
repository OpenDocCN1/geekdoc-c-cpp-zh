only in their return type, and the virtual machine will handle this situation correctly.

> **NOTE:** Bridge methods are not limited to generic types. We already noted in Chapter 5 that it is legal for a method to specify a more restrictive *return type* when overriding another method. For example:

```
public class Employee implements Cloneable
{
    public Employee clone() throws CloneNotSupportedException { . . . }
}
```

The `Object.clone` and `Employee.clone` methods are said to have *covariant return types*.

Actually, the `Employee` class has two clone methods:

```
Employee clone() // defined above
Object clone() // synthesized bridge method, overrides Object.clone
```

The synthesized bridge method calls the newly defined method.

+   - There are no generics in the virtual machine, only ordinary classes and methods.
+   - All type parameters are replaced by their bounds.
+   - Bridge methods are synthesized to preserve polymorphism.
+   - Casts are inserted as necessary to preserve type safety.

# ### 8.5.4 Calling Legacy Code

When Java generics were designed, a major goal was to allow interoperability between generics and legacy code. Let us look at a concrete example of such legacy. The Swing user interface toolkit provides a `JSlider` class whose "ticks" can be customized with labels that contain text or images. The labels are set with the call

```
void setLabelTable(Dictionary table)
```

The `Dictionary` class maps integers to labels. Before Java 5, that class was implemented as a map of `Object` instances. Java 5 made `Dictionary` into a generic class, but `JSlider` was never updated. At this point, `Dictionary` without type parameters is a raw type. This is where compatibility comes in.