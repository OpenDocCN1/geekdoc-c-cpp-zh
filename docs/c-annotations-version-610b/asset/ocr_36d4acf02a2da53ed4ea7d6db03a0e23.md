```
```cpp
{
    Strings tmp(other);
    // more to follow
    return *this;
}
```
```

You may think the optimization `operator=(String tmp)` is attractive, but let's postpone that for a little while (at least until section 9.7).

Now that we've done the copying part, what about the deleting part? And isn't there another slight problem as well? After all we copied all right, but not into our intended (current, `*this`) object.

At this point it's time to introduce *swapping*. Swapping two variables means that the two variables exchange their values. We'll discuss swapping in detail in the next section, but let's for now assume that we've added a member `swap(Strings &other)` to our class `Strings`. This allows us to complete `String`'s `operator=` implementation:

```
```cpp
Strings &operator=(Strings const &other)
{
    Strings tmp(other);
    swap(tmp);
    return *this;
}
```
```

This implementation of `operator=` is generic: it can be applied to every class whose objects are swap-pable. How does it work?

+   - The information in the `other` object is used to initialize a local `tmp` object. This takes care of the copying part of the assignment operator;
+   - Calling `swap` ensures that the current object receives its new values (with `tmp` receiving the current object's original values);
+   - When `operator=` terminates its local `tmp` object ceases to exist and its destructor is called. As it by now contains the data previously owned by the current object, the current object's original data are now destroyed, effectively completing the destruction part of the assignment operation.

Nice?

# ### 9.6.1 Swapping

Many classes (e.g., `std::string`) offer `swap` members allowing us to swap two of their objects. The *Standard Template Library* (STL, cf. chapter 18) offers various functions related to swapping. There is even a `swap` generic algorithm (cf. section 19.1.61), which is commonly implemented using the assignment operator. When implementing a `swap` member for our class `Strings` it could be used, provided that all of `String`'s data members can be swapped. As this is true (*why* this is true is discussed shortly) we can augment class `Strings` with a `swap` member:

```
```cpp
void Strings::swap(Strings &other)
{
    swap(d_string, other.d_string);
    swap(d_size, other.d_size);
}
```
```

Having added this member to `Strings` the copy-and-swap implementation of `String::operator=` can now be used.