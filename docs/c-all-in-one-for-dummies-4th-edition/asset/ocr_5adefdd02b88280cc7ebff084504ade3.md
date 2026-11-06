# # Chapter 5

# # Streaming Your Own Classes

The C++ stream classes can read and write all sorts of goodies, such as integers, characters, strings, floating-point numbers, and Boolean variables. But sooner or later, being able to stream one of your own classes (like the following) would be nice:

```
```cpp
MyClass x;
cout << x << endl;
```
```

C++ has a good reason not to have done this already: The compiler and library can't predict on their own how you want to stream your class using cout. (The example in the "Writing and reading structured data" section of Chapter 3 of this minibook shows one technique for accomplishing this task by overriding the << operator.) Here are some examples:

+   * The name of the class followed by the values of the public properties.
+   * The private properties.
+   * Derived values or some other information related to the class.