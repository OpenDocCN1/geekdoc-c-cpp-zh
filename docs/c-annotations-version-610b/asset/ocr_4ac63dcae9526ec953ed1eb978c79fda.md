function has irrevocably mutated the `PersonDb`’s data, thus losing the strong guarantee.

Rather than returning `d_data[idx]` by value it might be assigned to an external `Person` object before mutating `PersonDb`’s data:

```
void PersonData::erase(Person *dest, size_t idx)
{
    if (idx >= d_size)
        throw string("Array bounds exceeded");
    *dest = d_data[idx];
    Person *tmp = copyAllBut(idx);
    delete[] d_data;
    d_data = tmp;
    --d_size;
}
```

This modification works, but changes the original assignment of creating a member returning the original object. However, both functions suffer from a task overload as they modify `PersonDb`’s data and also return an original object. In situations like these the *one-function-one-responsibility* rule of thumb should be kept in mind: a function should have a single, well defined responsibility.

The preferred approach is to retrieve `PersonDb`’s objects using a member like `Person const & at(size_t idx) const` and to erase an object using a member like `void PersonData::erase(size_t idx)`.

# 10.9.3 The nothrow guarantee

Exception safety can only be realized if some functions and operations are guaranteed *not* to throw exceptions. This is called the *nothrow guarantee*. An example of a function that must offer the nothrow guarantee is the `swap` function. Consider once again the canonical overloaded assignment operator:

```
Class &operator=(Class const &other)
{
    Class tmp(other);
    swap(tmp);
    return *this;
}
```

If `swap` were allowed to throw exceptions then it would most likely leave the current object in a partially swapped state. As a result the current object’s state would most likely have been changed. As `tmp` has been destroyed by the time a catch handler receives the thrown exception it becomes very difficult (as in: impossible) to retrieve the object’s original state. Losing the strong guarantee as a consequence.

The `swap` function must therefore offer the nothrow guarantee. It must have been designed as if using the following prototype (don’t do this: see also section [10.6](#)):

```
void Class::swap(Class &other) throw();
```

Likewise, `operator delete` and `operator delete[]` offer the nothrow guarantee, and according to the **C++** standard destructors may themselves not throw exceptions (if they do their behavior is formally undefined, see also section [10.11](#) below).

Since the **C** programming language does not define the exception concept functions from the standard C library offer the nothrow guarantee by implication. This allowed us to define the generic `swap` function in section [9.6](#) using `memcpy`.

Operations on primitive types offer the nothrow guarantee. Pointers may be reassigned, references may be returned etc. etc. without having to worry about exceptions that might be thrown.