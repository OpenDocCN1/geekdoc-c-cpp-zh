The introduction of generics in Java 5 constitutes the most significant change in the Java programming language since its initial release. A major design goal was to be backwards compatible with earlier releases. As a result, Java generics have some uncomfortable limitations. You will learn about the benefits and challenges of generic programming in this chapter.

# ## 8.1 Why Generic Programming?

*Generic programming* means writing code that can be reused for objects of many different types. For example, you don’t want to program separate classes to collect String and File objects. And you don’t have to—the single class `ArrayList` collects objects of any class. This is one example of generic programming.

Actually, Java had an ArrayList class before it had generic classes. Let us investigate how the mechanism for generic programming has evolved, and what that means for users and implementors.

# ### 8.1.1 The Advantage of Type Parameters

Before generic classes were added to Java, generic programming was achieved with *inheritance*. The `ArrayList` class simply maintained an array of `Object` references:

```
public class ArrayList // before generic classes
{
    private Object[] elementData;

    public Object get(int i) { . . . }
    public void add(Object o) { . . . }
}
```

This approach has two problems. A cast is necessary whenever you retrieve a value:

```
ArrayList files = new ArrayList();
. . .
String filename = (String) files.get(0);
```

Moreover, there is no error checking. You can add values of any class:

```
files.add(new File(". . ."));
```

This call compiles and runs without error. Elsewhere, casting the result of `get` to a String will cause an error.