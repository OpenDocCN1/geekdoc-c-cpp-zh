the source `Array` to the target `Array`. Regardless of whether this is a self-assignment, the member function returns the current object (i.e., `*this` in line 52) as a constant reference; this enables cascaded `Array` assignments such as `x = y = z`, but prevents ones like `(x = y) = z` because `z` cannot be assigned to the `const Array` reference that’s returned by `(x = y)`. If self-assignment occurs, and function `operator=` did not test for this case, `operator=` would unnecessarily copy the elements of the `Array` into itself.

![](bbox=[0.118, 0.377, 0.195, 0.439])

# Software Engineering Observation 10.4

*A copy constructor, a destructor and an overloaded assignment operator are usually provided as a group for any class that uses dynamically allocated memory. With the addition of move semantics in C++11, other functions should also be provided, as you’ll see in Chapter 10.*

![](bbox=[0.118, 0.692, 0.192, 0.749])

# Common Programming Error 10.4

*Not providing a copy constructor and overloaded assignment operator for a class when objects of that class contain pointers to dynamically allocated memory is a potential logic error.*