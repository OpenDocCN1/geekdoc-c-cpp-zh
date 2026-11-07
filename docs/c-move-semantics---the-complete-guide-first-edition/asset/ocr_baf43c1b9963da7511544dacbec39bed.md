```
```cpp
...
int i = stk.top();           // do something else without using stk
assert(i == 42);             // should never fail
```
```

Although we do not know the value of stk after passing it with std::move() to foo(), we can use it as a valid stack as long as we use it only to hold our value 42 until we need it again.

Of course, it is up to you how far the guarantees you give go, but ensure that the users of your type are aware of these guarantees. Usually, they expect that your types give the same guarantee as the C++ library, so that you can use a moved-from object just like any other object of the type without knowing its value.

# ### 6.1.3 Broken Invariants

The C++ standard library defines what all moved-from objects being in a "valid but unspecified state" means as follows:

> > The value of an object is not specified except that the object’s invariants are met and operations on the object behave as specified for its type

Invariants are the guarantees that apply to all of the objects that can be created. With this guarantee, you can assume that a moved-from object is in a state that means that its invariants are not broken. You can use the object like a non-const reference parameter without knowing anything about the argument passed: you can call any operation that has no constraint or precondition and the effect/result of this call is as specified for any other object of this type.

For example, for a moved-from string, we can perform all operations that have no precondition:

+   - Ask for its size
+   - Print it out
+   - Iterate over the characters
+   - Convert it to a C string
+   - Assign a new value
+   - Append a character

Furthermore, all of these functions still have the usual specified semantics:

+   - The returned size can be used to safely call the index operator.
+   - The returned size matches the number of characters when iterating over them.
+   - The printed characters match the sequence of characters when iterating over them.
+   - Appending a character will place that character at the end of the value (without knowing whether and which other characters are in front).

Programmers can make use of these guarantees (see the std::stack<> example above).

However, sometimes you have to explicitly ensure that intended invariants are not broken. The default special move member functions might not work properly. We will discuss examples in the following subsections.