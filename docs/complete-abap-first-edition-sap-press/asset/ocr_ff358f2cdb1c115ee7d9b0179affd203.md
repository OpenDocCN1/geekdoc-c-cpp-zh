To understand polymorphism, you first need to understand static and dynamic types. We'll then look at how to use casting when a static type source reference object isn't the same as the target reference object. From there, we'll discuss how to use dynamic binding with the `CALL` method before finally looking at implementing multiple inheritances using interfaces.

# ### 8.4.1 Static and Dynamic Types

The *static type* of an object (reference variable) is the class type that is used to define an object. For example, in *Listing 8.24*, the `oref` reference is defined by referring to the `cl_class` class. In this case, the static type of the `oref` object is the `cl_class` class as it's statically defined in the code.

```
```abap
CLASS cl_class DEFINITION.
  PUBLIC SECTION.
  METHODS meth.
ENDCLASS.
CLASS cl_class IMPLEMENTATION.
  METHOD meth.
  ENDMETHOD.
ENDCLASS.
DATA oref TYPE REF TO cl_class.
```
```

# **Listing 8.24 Code Defining Reference Object**

Sometimes, you may want to assign one reference object to another reference object that doesn't share the same static type. For example, because instances of classes in an inheritance tree are interchangeable, you can assign the instance of the subclass to the instance of the superclass, as shown in *Listing 8.25*, by using the `parent = child` statement.

```
```abap
CLASS cl_parent DEFINITION.
  PUBLIC SECTION.
  METHODS meth1.
  METHODS meth2.
ENDCLASS.
CLASS cl_parent IMPLEMENTATION.
  METHOD meth1.
    WRITE 'In method1 of parent'.
  ENDMETHOD.
  METHOD meth2.
    WRITE 'In method2 of parent'.
  ENDMETHOD.
ENDCLASS.
```
```