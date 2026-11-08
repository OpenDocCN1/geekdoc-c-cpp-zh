Because the function `incrementY` is static and public, the following statement is legal:

```
illustrate::incrementY();
```

Similarly, because the member variable `count` is static and public, the following statement is legal:

```
illustrate::count++;
```

Next, we elaborate on static member variables a bit more. Suppose that you have a class, say, myClass, with member variables (static as well as non-static). When you create objects of type myClass, only non-static member variables of the class myClass become the member variables of each object. For each static member variable of a class, C++ allocates only one memory space. All myClass objects refer to the same memory space. In fact, static member variables of a class exist even when no object of that class type exists. You can access the public static member variables outside of the class, as explained earlier in this section.

Next, we explain how memory space is allocated for static and non-static member variables of a class.

Suppose that you have the class illustrate, as given in Example 10-10. Memory space then exists for the static member variables y and count.

Consider the following statements:

```
illustrate illusObject1(3);    //Line 1
illustrate illusObject2(5);    //Line 2
```

The statements in Lines 1 and 2 declare illusObject1 and illusObject2 to be illustrate type objects (see Figure 10-12).

![](bbox=[0.224, 0.696, 0.899, 0.813])

**FIGURE 10-12** illusObject1 and illusObject2

Now, consider the following statements:

```
illustrate::incrementY();
illustrate::count++;
```