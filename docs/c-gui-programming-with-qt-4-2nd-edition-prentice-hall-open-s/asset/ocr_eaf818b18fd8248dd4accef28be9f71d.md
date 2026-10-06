* Reference types: These classes are used as Integer (in Java), String, and MyOwnClass. Instances are created using new. The assignment operator copies only a reference to the object; to obtain a deep copy, we must call clone() (in Java) or Clone() (in C#). For example:

```
Integer i = new Integer(5);
Integer j = new Integer(10);
i = j.clone();
```

In C++, all types can be used as "reference types", and those that are copyable can be used as "value types" as well. For example, C++ doesn't need any Integer class, because we can use pointers and new as follows:

```
int *i = new int(5);
int j = new int(10);
i = *j;
```

Unlike Java and C#, C++ treats user-defined classes in the same way as built-in types:

```
Point2D *i = new Point2D(5, 5);
Point2D j = new Point2D(10, 10);
i = *j;
```

If we want to make a C++ class copyable, we must ensure that our class has a copy constructor and an assignment operator. The copy constructor is invoked when we initialize an object with another object of the same type. C++ provides two equivalent syntaxes for this:

```
Point2D i(20, 20);

Point2D j(i);      // first syntax
Point2D k = i;      // second syntax
```

The assignment operator is invoked when we use the assignment operator on an existing variable:

```
Point2D i(5, 5);
Point2D j(10, 10);
j = i;
```