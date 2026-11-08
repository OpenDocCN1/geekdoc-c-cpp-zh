Destructor calls through a pointer or a reference parameter should have dynamic binding, so the destructor that is called will be selected at runtime. This makes the destructor in every class derived from the base class virtual, in spite of the derived class destructors having different names; destructors are treated as a special case for this purpose.

You can see this effect by adding the virtual keyword to the destructor declaration in the Box class of Ex15_07:

```
```cpp
export class Box
{
public:
    Box() : Box{1.0, 1.0, 1.0} {}
    Box(double l, double w, double h) : m_length {l}, m_width {w}, m_height {h} {}

    virtual ~Box() { std::cout << "Box destructor called" << std::endl; }

    // Remainder of the Box class as before...
};
```
```

The destructors of all the derived classes will automatically be virtual as a result of declaring a virtual base class destructor. If you run the example again, the output will confirm that this is so. If it weren't the output message we added for this function would have been an empty {} block. Instead of using such an empty block, though, we recommend you declare the destructor using the = default. This makes it much more visible that a default implementation is used. For our Box class, you would then write the following:

```
```cpp
virtual ~Box() = default;
```
```

The default keyword can be used for all members the compiler would normally generate for you. This includes destructors but also, as you saw earlier, constructors and assignment operators. Note that compiler-generated destructors are never virtual, unless you explicitly declare them as such.

> **Tip**  When polymorphism is expected (or even just possible), your class must have a virtual destructor to ensure that your objects are always properly destroyed. This implies that as soon as a class has at least one virtual member function, its destructor should be made virtual as well. (The only time you do not have to follow this guideline is if the nonvirtual destructor is either protected or private, but these are rather exceptional cases.)

# Converting Between Pointers to Class Objects

You can implicitly convert a pointer to a derived class to a pointer to a base class, and you can do this for both direct and indirect base classes. For example, let's first define a smart pointer to a Carton object:

```
```cpp
auto carton{ std::make_unique<Carton>(30, 40, 10) };
```
```

You can convert the pointer that is embedded in this smart pointer implicitly to a pointer to Box, which is a direct base class of Carton:

```
```cpp
Box* box_pointer {carton.get()};
```
```