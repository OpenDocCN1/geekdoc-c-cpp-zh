However, note that we have additional requirements and guarantees that apply to the move constructor and move assignment operator of all containers except std::array<>. These requirements and guarantees essentially mean that moved-from containers are usually empty.

# Container Guarantees for Move Constructors

For the move constructor:

```
ContainerType cont1{...};
ContainerType cont2{std::move(cont1)};    // move the container
```

the C++ standard specifies constant complexity. This means that the duration of a move does not depend on the number of elements.

With this guarantee, implementers have no other option but to steal the memory of elements as a whole from the source object cont1 to the destination object cont2, leaving the source object cont1 in an initial/empty state.

You might argue that the move constructor could also create a new value in the source object but that does not make much sense because it only makes the operation slower.

For vectors, providing a value in a moved-from object is even indirectly forbidden because the move constructor of std::vector<> guarantees never to throw:

```
template<typename T, typename Allocator = allocator<T>>
class vector {
public:
    ...
    vector(const vector&);                 // copy constructor
    vector(vector&&) noexcept;             // move constructor
    ...
};
```

In summary, effectively we have the following guarantees for containers after using them as source in a move constructor:

+   - For vectors, it is essentially required that the moved-from container is empty.
+   - For the other containers (except std::array<>), being empty is not strictly required but it usually makes no sense to implement anything else.

# Container Guarantees for Move Assignment Operators

For the move assignment operator:

```
ContainerType cont1{...}, cont2{...};
cont2 = std::move(cont1);                 // move assign the container
```

the C++ standard guarantees that this operation either overwrites or destroys each element of the destination object cont2. This guarantees that all resources that the elements of the destination container dest2 own on entry are released. As a consequence, there are only two ways to implement a move assignment:

+   - Destroy the old elements and move the whole contents of the source to the destination (i.e., move the pointer to the memory from the source to the destination).