```
```cpp
int* intptr;
float* floatptr;
intptr = reinterpret_cast<int*>(m);
floatptr = reinterpret_cast<float*>(x);
```
```

# The dynamic_cast Operator

The dynamic cast is used to cast the type of an object at runtime. Its main application is to perform casts on polymorphic objects. Recall that polymorphic objects are created by base classes that contain virtual functions. It takes the form:

```
`dynamic_cast<type>(object)`
```

The *object* is a base class object whose type is to be checked and casted. It casts the type of object to *type*. It never performs an invalid conversion. It checks that the conversion is legal at runtime. If the conversion is not valid, it returns NULL.

The *type* must be a pointer or a reference to a defined class type. The *argument* object must be expression that resolves to a pointer or reference. The use of the operator **dynamic_cast()** is also called a *type-safe downcast*.

# The typeid Operator

We can use the **typeid** operator to obtain the types of unknown objects, such as their class name at runtime. For example, the statement

```
`char *objectType = typeid(object).name();`
```

will assign the type of “object” to the character array **objectType** which can be printed out, if necessary. To do this, it uses the **name()**