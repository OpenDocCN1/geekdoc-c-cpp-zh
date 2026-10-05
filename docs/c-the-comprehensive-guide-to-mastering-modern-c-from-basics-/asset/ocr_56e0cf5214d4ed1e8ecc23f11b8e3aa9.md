```
more.value = 7;
System.out.println(data.value); // always 7
```

# ### Listing 3.1 Java: A small Java example with the ubiquitous object references.

data and more are references. In fact, they are more like pointers in C++, because they can also assign the null pointer null to data, which would not be possible with references in C++. The assignment data = more means that data and more now reference the same instance. In C++, you would rather write:

```
Data(5);
Data(6);
data = =
more.value = 7;
cout << data.value << '\n'; // still 6
```

# ### Listing 3.2 C++ In C++, you have values instead of references.

Here, and more are separate values. Assuming more{6} resulted in the initialization more.value=6, then data.value still contains the 6 even after the assignment of more.value=7.

And if you use heap and pointers with new in C++ to emulate Java behavior, don't forget that you don't have a garbage collection, but have to release the heap again somew. To do this, use either an auxiliary class such as shared_ptr (recommended) or an explicit delete:

```
// https://godbolt.org/z/WM11Gs6sz
auto data = make_shared<Data>(5);
auto more = make_shared<Data>(6);
data = more;
```