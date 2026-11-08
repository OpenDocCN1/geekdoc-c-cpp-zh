Similarly, I call `Tree::stats()` at the end. Again, only static data fields are accessed. And the output

```
Constructed:+4 Destructed:-3
```

proves that each instance accessed the same counter variables in its constructor or destructor. The count is correct because all Tree temp objects in the loop were also destroyed again. Only the local birch variable still exists at the time of the `stats()` call.

# Copy Constructor and Move Constructor

How to make a class that copies itself is detailed in Chapter 16. At this point, you should know that classes can be copied. Sometimes the compiler can set the rules for this, and sometimes you want or need to do it yourself. To do this, declare this constructor:

```
Keyboard(const Keyboard&);
```

In the definition, you then specify how the copying should be done. If you explicitly want to prevent a copy from being possible, write the declaration like this:

```
Keyboard(const Keyboard&) = delete;
```

The same applies to moving. The declaration that you use to declare and simultaneously prevent the move is this:

```
Keyboard(Keyboard&&) = delete;
```

However, this is implicit if you have specified the copy constructor. For more on this, see Chapter 16.

# 13.5  Remote Initialization or “static inline” Data Fields

Assume you have defined a `Tree` class in the `tree.hpp` header and used the header multiple times in your program. Then you must ensure that the initialization of the static data fields is done in exactly one *.cpp file and not in the *.hpp file as they would otherwise be defined multiple times.

Therefore, starting from C++17, in addition to `static`, write the `inline` keyword and set the field directly—that is, the declaration and definition together. The compiler ensures unique initialization:

```
class Tree {
    static inline size_t countConstructed_ = 0;
    static inline size_t countDestructed_ = 0;
    // ...
```