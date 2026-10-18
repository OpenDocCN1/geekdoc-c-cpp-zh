In this version, we simply return a copy of the `char_counter_vec` local object. That is, a temporary local object is created from `char_counter_vec` using the copy constructor, to be returned as a return value at line [41].³ But in modern C++, if an object has a move constructor, the compiler will be smart enough to figure out the situation and call it instead of making heavy and usually unnecessary local copies of an object. In short, move semantics allow the simple exchange of pointers to data instead of moving the entire data pool, as we will discuss (see Section 4.6.4).

Obviously, the problem of referring to live objects is also important when dealing with pointers. In this case, we have another potential pitfall associated with object ownership passing from pointer to pointer.

Every rose has its thorns; and because of their value syntax but pointer semantics, some programmers consider references confusing (see https://google.github.io/styleguide/cppguide.html). We can be surprised when calling a function with an object as its parameter since this object’s state can be stealthy changed in the function when passing an object with a reference (see Section 3.14.2.2).

# 4.6 Example Project – Mastering Class Members with the *TheCube* Class

There are many different types of classes, since they represent a variety of real objects. Nevertheless, common construction patterns can be identified for a broad group of them. In this section, we will investigate the details of a class for modeling cubes of data like the one shown in Figure 4.6a. In this section, we will learn about the following:

+   - How to define a container class to store data organized as a 3D cube (a tensor)
+   - Class special member functions
+   - Deep vs. shallow copying
+   - Implementation of move semantics

![](bbox=[0.253, 0.615, 0.752, 0.837])

**Figure 4.6** Illustration of TheCube and memory allocation in its internal data buffer.

> ³ There is no need to perform a cast on a return value with `std::move` – a modern C++ compiler will know what to do.