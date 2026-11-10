![](bbox=[0.142, 0.103, 0.851, 0.439])

**Figure 9.18** Raising Exception for ZDEMO_GET_MATERIAL_DESCRIPTION

Now that you know how to define exception classes globally, let's look at local exception classes.

# 9.3.4 Defining Exception Classes Locally

Local exception classes can be defined to work with exceptions within the program locally. The syntax to define a local exception class is similar to that for a regular class, except that it should inherit `CX_STATIC_CHECK`, `CX_DYNAMIC_CHECK`, or `CX_NO_CHECK`, as shown in Listing 9.7. The naming convention `LCX_` is used for local exception classes.

In Listing 9.7, we define a `LCX_NO_MATERIAL` local exception class, which inherits from the `CX_STATIC_CHECK` class. Apart from their visibility, working with local exception classes is similar to working with global exception classes.

```
CLASS lcx_no_material DEFINITION INHERITING FROM cx_static_check.
ENDCLASS.
CLASS lcx_no_material IMPLEMENTATION.
ENDCLASS.
```

**Listing 9.7** Local Exception Class