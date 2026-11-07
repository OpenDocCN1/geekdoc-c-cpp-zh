Now, assume we'd like to copy x into a new object named y. If the copy constructor simply copied the pointer in x into the target object y's pointer, both would point to the same dynamically allocated memory, as in the right side of the diagram. The first destructor to execute would delete the memory that is shared between these two objects. The other object's pointer would then point to memory that's no longer allocated. This situation is called a dangling pointer. Typically, this would result in a serious runtime error (such as early program termination) if the program were to dereference that pointer—accessing deleted memory is undefined behavior.

# Deep Copy

In classes that manage their own resources, copying must be done carefully to avoid the pitfalls of shallow copies. Classes that manage their objects' resources should define their own copy constructor and overloaded copy assignment operator to perform *deep copies*. The following diagram shows that after the object x is deep copied into the object y, both objects have their own copies of the dynamically allocated array containing 10, 20 and 30. Not providing a copy constructor and overloaded assignment operator for a class when objects of that class contain pointers to dynamically allocated memory is a potential logic error.

![](bbox=[0.225, 0.445, 0.782, 0.58])

# Implementing the Copy Constructor

Line 21 of Fig. 11.4

```
```cpp
MyArray(const MyArray& original); // copy constructor
```
```

declares the class's copy constructor (defined lines 32–41). Its argument must be a **const reference** to prevent the constructor from modifying the argument object's data.

```
```cpp
31 // copy constructor: must receive a reference to a MyArray
32 MyArray::MyArray(const MyArray& original)
33     : m_size(original.size()),
34       m_ptr{std::make_unique<int[]>(original.size())} {
35     std::cout << "MyArray copy constructor\n";
36
37     // copy original's elements into m_ptr's underlying int array
38     const std::span<const int> source{
39         original.m_ptr.get(), original.size()};
40     std::copy(std::begin(source), std::end(source), m_ptr.get());
41 }
42
```
```