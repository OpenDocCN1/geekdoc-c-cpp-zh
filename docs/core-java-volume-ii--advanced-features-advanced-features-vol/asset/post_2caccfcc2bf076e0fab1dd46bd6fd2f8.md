
> **NOTE:** Annotations for local variables can only be processed at the source level. Class files do not describe local variables. Therefore, all local variable annotations are discarded when a class is compiled. Similarly, annotations for packages are not retained beyond the source level.

## 8.4.4 Annotating Type Uses

A declaration annotation provides some information about the item being declared. For example, in the declaration

```java
public User getUser(@NonNull String userId)
```

it is asserted that the `userId` parameter is not null.

> **NOTE:** The `@NonNull` annotation is a part of the Checker Framework (https://checkerframework.org). With that framework, you can include assertions in your program—for example, that a parameter is non-null or that a String contains a regular expression. A static analysis tool then checks whether the assertions are valid in a given body of source code.

Now, suppose we have a parameter of type `List<String>`, and we want to express that all of the strings are non-null. That is where type use annotations come in. Place the annotation before the type argument: `List<@NonNull String>`.

Type use annotations can appear in the following places:

- With generic type arguments: `List<@NonNull String>`, `Comparator<@NonNull String> reverseOrder()`.
- In any position of an array: `@NonNull String[][] words` (`words[i][i]` is not null), `String @NonNull [] words` (words is not null), `String[] @NonNull [] words` (words[i] is not null).
- With superclasses and implemented interfaces: `class Warning extends @Localized Message`.
- With constructor invocations: `new @Localized String(...)`.
- With casts and instanceof checks: `(@Localized String) text`, `if (text instanceof @Localized String)`. The annotations are only for use by external tools. They have no effect on the behavior of a cast or an instanceof check.
- With exception specifications: `public String read() throws @Localized IOException`.
- With wildcards and type bounds: `List<@Localized String> extends Message`, `List<? extends @Localized Message>`.
- With method and constructor references: `@Localized Message::getText`.

```java
public class Point
{
    public boolean equals(@ReadOnly Point this, @ReadOnly Object other) { . . . }
}
```

The first parameter is called the *receiver parameter*. It must be named `this`. Its type is the class that is being constructed.

> **NOTE:** You can provide a receiver parameter only for methods, not for constructors. Conceptually, this reference in a constructor is not an object of the given type until the constructor has completed. Instead, an annotation placed on the constructor describes a property of the constructed object.

A different hidden parameter is passed to the constructor of an inner class, namely the reference to the enclosing class object. You can make that parameter explicit as well:

```java
public class Sequence
{
    private int from;
    private int to;

    class Iterator implements java.util.Iterator<Integer>
    {
        private int current;
        public Iterator(@ReadOnly Sequence Sequence.this)
        {
            this.current = Sequence.this.from;
        }
        . . .
    }
    . . .
}
```

The parameter must be named just like when you refer to it, `EnclosingClass.this`, and its type is the enclosing class.

## 8.5 Standard Annotations

A number of annotation interfaces are defined in the `java.lang`, `java.lang.annotation`, and `javax.annotation` packages. Four of them are meta-annotations that describe the behavior of annotation interfaces. The others are regular annotations that you can use to annotate items in your source code. Table 8.2 shows these annotations. We’ll discuss them in detail in the following two sections.

### 8.5.1 Annotations for Compilation

The `@Deprecated` annotation can be attached to any items whose use is no longer encouraged. The compiler will warn you when you use a deprecated item. This annotation has the same role as the `@deprecated` Javadoc tag. However, the annotation persists until runtime.

> **NOTE:** The `jar` utility that is part of the JDK can scan a set of JAR files for deprecated elements.

The `@SuppressWarnings` annotation tells the compiler to suppress warnings of a particular type, for example:

```java
@SuppressWarnings("unchecked")
```

The `@Override` annotation applies only to methods. The compiler checks that a method with this annotation really overrides a method from the superclass. For example, if you declare

```java
public class MyClass
{
    @Override public boolean equals(MyClass other);
    . . .
}
```

then the compiler will report an error. After all, the equals method does *not* override the equals method of the Object class because that method has a parameter of type Object, not MyClass.

The `@Generated` annotation is intended for use by code generator tools. Any generated source code can be annotated to differentiate it from programmer-created code. For example, a code editor can hide the generated code, or a code generator can remove older versions of generated code. Each annotation must contain a unique identifier for the code generator. A date string (in ISO 8601 format) and a comment string are optional. For example,

```java
@Generated("com.horstmann.beanproperty", "2008-01-04T12:08:56.235-0700");
```

### 8.5.2 Annotations for Managing Resources

The `@PostConstruct` and `@PreDestroy` annotations are used in environments that control the lifecycle of objects, such as web containers and application servers. Methods tagged with these annotations should be invoked immediately after an object has been constructed or immediately before it is being removed.

The `@Resource` annotation is intended for resource injection. For example, consider a web application that accesses a database. Of course, the database access information should not be hardwired into the web application. Instead, the web container has some user interface for setting connection parameters and a JNDI name for a data source. In the web application, you can reference the data source like this:

```java
@Resource(name="jdbc/mydb")
private DataSource source;
```

When an object containing this field is constructed, the container “injects” a reference to the data source.

### 8.5.3 Meta-Annotations

The `@Target` meta-annotation is applied to an annotation, restricting the items to which the annotation applies. For example,

```java
@Target({ElementType.TYPE, ElementType.METHOD})
public @interface BugReport
```

Table 8.3 shows all possible values. They belong to the enumerated type ElementType. You can specify any number of element types, enclosed in braces.

**Table 8.3** Element Types for the @Target Annotation

| Element type | Annotation Applies To |
|---|---|
| ANNOTATION_TYPE | Annotation type declarations |
| PACKAGE | Packages |
| TYPE | Classes (including enum) and interfaces (including annotation types) |
| METHOD | Methods |
| CONSTRUCTOR | Constructors |
| FIELD | Fields (including enum constants) |
| PARAMETER | Method or constructor parameters |
| LOCAL_VARIABLE | Local variables |
| TYPE_PARAMETER | Type parameters |
| TYPE_USE | Uses of a type |

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_505_0.png)

Figure 8.2 Documented annotations

The `@Inherited` meta-annotation applies only to annotations for classes. When a class has an inherited annotation, then all of its subclasses automatically have the same annotation. This makes it easy to create annotations that work as marker interfaces, such as Serializable.

In fact, an annotation `@Serializable` would be more appropriate than the Serializable marker interface with no methods. A class is serializable because there is runtime support for reading and writing its fields, not because of any principles of object-oriented design. An annotation describes this fact better than does interface inheritance. Of course, the Serializable interface was created in JDK 1.1, long before annotations existed.

Suppose you define an inherited annotation `@Persistent` to indicate that objects of a class can be saved in a database. Then the subclasses of persistent classes are automatically annotated as persistent.

```java
@Inherited @interface Persistent { }
@Persistent class Employee { . . . }
class Manager extends Employee { . . . } // also @Persistent
```

When the persistence mechanism searches for objects to store in the database, it will detect both Employee and Manager objects.
