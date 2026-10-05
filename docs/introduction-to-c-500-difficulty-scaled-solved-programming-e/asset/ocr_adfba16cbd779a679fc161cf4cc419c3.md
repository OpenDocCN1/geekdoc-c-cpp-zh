C++11 also provides the alignas specifier, which can be used to specify the alignment of the type.
For example:

```
struct alignas(64) A
{
    int i;
}
cout << alignof(A) << '\n'; // The code outputs 64.
```

Each variable will be aligned to a boundary of 64 bytes. Note that the number of bytes should be a valid alignment, such as a power of 2.

# Initializing a Structure

The common method to access a structure member is to write the name of the structure variable followed by the . operator and the name of the member. For example, the following program displays the members of the b members:

```
#include <iostream> // Example 13.2
#include <string>

struct Book
{
    std::string title;
    int year;
    float price;
}

int main()
{
    Book b;

    b.title = "Literature";
    b.year = 2016;
    b.price = 10.85;
    std::cout << b.title << ' ' << b.year << ' ' << b.price << '\n';
    return 0;
}

```

Besides the . operator, you'll learn how to use the -> operator to access the members of a structure.
Note that when b declared members get initial values. In particular, with ordinary local variables, arithmetic members are initialized with random values, while class type members are initialized with the default value for the class. For example, the default value for the string class is "".

A structure variable can be initialized when it is declared. The declaration is followed by a list of initializers in braces. The list must appear in the same order as the members of the structure and match their data types. The list values are separated by a comma and must not be more values than members. Consider the following declaration:

```
Book b = {"Literature", 2016, 10.85};
```

The value of b.title becomes "Literature", b.year becomes 2016 and b.price becomes 10.85.