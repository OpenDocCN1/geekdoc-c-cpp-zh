In the next section of the `TComplex` definition, we see the group of *special member functions*. This group can contain the following items:

+   - A default constructor to create and initialize an object with no external parameters
+   - Parametric constructor(s) to create and initialize an object with parameters
+   - A copy constructor to create and initialize an object based on another object of the same type
+   - An assignment operator to copy the state from another object of the same type
+   - A destructor to deallocate whatever was allocated during an object’s lifetime
+   - A move assignment, which is usually more efficient than a copy assignment because we can use data from the supplied object (Section 4.6.4)
+   - A move constructor to create and initialize an object, which can be more efficient than a copy constructor because we can use data from the supplied object (Section 4.6.4)
+   - Type-converting constructor(s) that create and initialize an object based on a passed parameter of a different type than its class (similar to the copy constructor)

As we have already seen, in most classes, few of these are needed. Some are for special occasions, as we will explain later. Also, some of them can be automatically deduced and implemented by the compiler, as we have seen. Returning to `TComplex`, its default constructor is on line [26], in the public section of the class beginning on line [21]. The characteristic part is the constructor’s initializer list, on line [27]. Its role is to call the constructors of its member data objects. If it is omitted, then the default constructors of the members are called. In that case initialization is possible but less efficient, since an object is first created with its default constructor, and then initialized as on line [29].

The definition of the parametric constructor begins on line [36]. It takes two arguments, which are immediately used in the constructor’s initializer list in the same line. Not surprisingly, in this case, the parametric constructors of the member objects are invoked, providing the appropriate parameters.

When designing a class, sometimes we have the option of not providing any constructors, since the data will be initialized using initialization lists. This is the rule of zero, explained in Section 3.9. But a decision to explicitly provide a parametric constructor has implications. More concretely, when we declare (write) a special member function other than the default constructor, the compiler will suppress the generation of other special functions. Therefore, if we decide to add a declaration of the parametric constructor or a destructor, we should *explicitly add all six other special functions*. This is called the *rule of six* (or five, depending on what we count). And this is exactly what we do here: the copy constructor is declared on line [43], the assignment operator on line [49], and the destructor on line [54]. In all of these functions, we use `=default`, since the default functionality is all we need – that is, data members are copied if necessary. Also, we skipped the special move functions, since we only have two small data members and so there is nothing to gain from move semantics. We will explain the construction and operations of these special members in upcoming sections.

```
```cpp
public:

    ////////////////////////////////////////////////
    // Default constructor
    ////////////////////////////////////////////////
    TComplex( void )
        :  fRe( 0.0 ), fIm( 0.0 )    // special data initialization
```
```