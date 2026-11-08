# Class Template Instantiation

The compiler instantiates a class template as a result of a definition of an object that has a type produced by the template. Here's an example:

```
Array<int> data {40};
```

When this statement is compiled, a definition for the Array<int> class is created where every occurrence of T in the template is substituted with int. But there's one subtlety. The compiler compiles only the member functions that your program uses, so you basically may not get the entire class that would be produced by a simple substitution for the template parameter. On the basis of just the definition for our object, data, the instantiated Array<int> class would thus be equivalent to the following:

```
class Array<int>
{
public:
    explicit Array(size_t size);  // Constructor
    ~Array();                     // Destructor

private:
    int* m_elements;              // Array of type int
    size_t m_size;                // Number of array elements
};
```

You can see that the instantiated class only has two member functions: the constructor and the destructor. The compiler won't create instances of anything that isn't required to create or destruct the object, and it won't include parts of the template that aren't needed in the program.

Of course the declaration of data causes the constructor Array<int>::Array(size_t_t) to be called as well, so after instantiating the class definition the compiler also instantiates a definition for the constructor for the Array<int> class from the corresponding member template:

```
Array<int>::Array(size_t_t size) : m_elements {new int[size]}, m_size {size}
{}
```

Once the data object inevitably goes out of scope, the compiler analogously instantiates the destructor for the Array<int> class as well.

> **Note**  This so-called *lazy instantiation* trait of member function templates implies that you can in fact create and use an Array<T> object for a type T whose objects cannot be copied (such as for instance Array<std::unique_ptr<T>>, as long as you do not use the copy constructor or copy assignment operator. It also implies, though, that coding errors in class member templates may go undetected until you first use them. We will give you some pointers in the next subsection on how you can quickly test for such errors.

If the instantiation of a class template arises as a by-product of declaring an object, it is referred to as an *implicit instantiation* of the template. This terminology also distinguishes it from an *explicit instantiation* of a template, which as seen in the next subsection behaves a little differently.