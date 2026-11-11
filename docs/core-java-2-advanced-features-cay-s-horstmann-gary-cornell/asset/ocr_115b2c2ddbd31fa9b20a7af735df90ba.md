```
```java
public @interface BugReport
{
    String assignedTo() default "[none]";
    int severity();
}
```
```

All annotation interfaces implicitly extend the `java.lang.annotation.Annotation` interface.
That interface is a regular interface, *not* an annotation interface. See the API
notes at the end of this section for the methods provided by this interface. You
cannot extend annotation interfaces. In other words, all annotation interfaces di-
rectly extend `java.lang.annotation.Annotation`. You never supply classes that implement
annotation interfaces.

The methods of an annotation interface have no parameters and no throws clauses.
They cannot be default or static methods, and they cannot have type parameters.

The type of an annotation element is one of the following:

+   - A primitive type (`int`, `short`, `long`, `byte`, `char`, `double`, `float`, or `boolean`)
+   - `String`
+   - Class (with an optional type parameter such as `Class<? extends MyClass>`)
+   - An enum type
+   - An annotation type
+   - An array of the preceding types (an array of arrays is not a legal element type)

Here are examples of valid element declarations:

```
```java
public @interface BugReport
{
    enum Status { UNCONFIRMED, CONFIRMED, FIXED, NOTABUG };
    boolean showStopper() default false;
    String assignedTo() default "[none]";
    Class<?> testCase() default Void.class;
    Status status() default Status.UNCONFIRMED;
    Reference ref() default @Reference(); // an annotation type
    String[] reportedBy();
}
```
```

| `java.lang.annotation.Annotation` 5.0 |
|---|
| • `Class<?> extends Annotation` annotationType()  
  returns the Class object that represents the annotation interface of this annotation object. Note that calling `getClass` on an annotation object would return the actual class, not the interface. |