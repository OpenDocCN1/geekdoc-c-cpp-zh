```
```cpp
{
    std::shared_ptr<Foo> foo; //
    ~Bar() { std::cout << "~Bar\n";}
};

void CyclicPointersProblem_Test( void )
{
    auto foo = make_shared< Foo >();
    foo->bar = make_shared< Bar >();

    foo->bar->foo = foo;        // oops, a circle ...
}
```
```

Remove the circular dependency between the objects. Hint: change the type of the smart pointer on line [16].

+   5. Design and implement a simple memory-allocation method for an embedded system. For safety reasons, a single statically allocated memory block can be used from which all partitions resulting from memory requests are created. Hint: read about and then implement the buddy algorithm (https://en.wikipedia.org/wiki/Buddy_memory_allocation).
+   
+   6. Design and implement a class to represent a submatrix (https://en.wikipedia.org/wiki/Matrix_(mathematics)) in a matrix object using the proxy pattern, presented in Section 4.15.5. The proxy has no data of its own but operates on the data of its associated matrix. But it defines its own local coordinate system and behaves like any other matrix. Hint: after making some modifications to the EMatrix class in Listing 4.7, derive a proxy class to represent submatrices. Such a proxy should not allocate its own data but should be constructed with a reference to its associated matrix. Accessing an element in the submatrix should result in the data coordinates being transformed to the coordinate system of the associated matrix.