+   - `Type[] getActualTypeArguments()`  
+     gets the type parameters with which this parameterized type was declared.
+   - `Type getOwnerType()`  
+     gets the outer class type if this is an inner type, or null if this is a top-level type.

# ***java.lang.reflect.GenericArrayType*** 5

+   - `Type getGenericComponentType()`  
+     gets the generic component type with which this array type was declared.

You now know how to use generic classes and how to program your own generic classes and methods if the need arises. Just as importantly, you know how to decipher the generic type declarations that you may encounter in the API documentation and in error messages. For an exhaustive discussion of everything there is to know about Java generics, turn to Angelika Langer’s excellent list of frequently (and not so frequently) asked questions at [http://angelikalanger.com/GenericsFAQ/JavaGenericsFAQ.html](http://angelikalanger.com/GenericsFAQ/JavaGenericsFAQ.html).

In the next chapter, you will see how the Java collections framework puts generics to work.