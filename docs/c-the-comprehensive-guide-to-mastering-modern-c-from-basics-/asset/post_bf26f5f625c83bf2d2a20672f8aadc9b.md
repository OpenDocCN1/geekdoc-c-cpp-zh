
```cpp
std::vector<Image> collection = loadCollection(false);
}
```

# **Listing 16.20** The class probably contains large amounts of data that are expensive to copy. But what is being copied here?

I have written a sample data type Image that likely holds large amounts of data in data. The compiler-generated operations for copy and assignment will completely copy this data field from the source to the target. So the data is duplicated after copying: I expect that, and thus it is fine.

Does it surprise you, then, when I tell you that at no point in Listing 16.20 are images duplicated in data? If not, then you either have already read something about move operations or expect too much from C++. I would like to illustrate how duplicate data could exist due to copying, and explain why this is not the case here:

- With Image{"MonaLisa.png"}, I create a new Image including its data. The push_back of vector takes its Image and places it where it stores its own data. This is a good candidate for a complete copy.

- With return result; I return the vector by value. What was previously a local variable is to be passed outside. In this case, it should be stored in another variable with collection = ... Such a scenario is another very good candidate for a copy—which here would be the copy of all vector-Image elements.

A vector has its own area where it stores its data. The new Image instances within loadCollection() are, of course, unaware of this and certainly store their data elsewhere. The push_back method of vector copies this data to where the vector wants it. The good news is that this copy can be omitted under certain circumstances—as in this example. vector can save the expensive copying of data for objects designed with Image. To achieve this, it is—as always—sufficient to use only built-in types, standard containers, or most types from the standard library, and then to define a copy constructor, destructor, or assignment operator.[40]

After return result;, it no longer makes sense to keep result as a local variable. When leaving the function, result is discarded; the destructor is called, and all contents are destroyed. It is good that the content was copied to collection beforehand for the return. Should you first make a complete copy and then destroy the original? This is not necessary in C++ either. In the case shown here, the content of result can be directly transferred—moved—to collection. This effect during return is called copy elision.

Neither is self-evident and both are subject to certain conditions. C++ can in no way forgo calling the destructor of result as that would contradict the RAII principles. And when the destructor is called, you can expect the data fields to be removed as well. The solution to the puzzle is that a special form of copying is applied—not the one you already know, but one that only works with temporary values.

The && symbol denotes a special form of reference, the temp-value reference (technically, the rvalue reference). For the moment, please consider this like the normal reference &, but remember that when dealing with moving you need &&:

- Image(Image&& other)—the move constructor Like the copy constructor, except that other is not const. Therefore, its data can be taken away from it. Used by the compiler only when other will not exist for much longer, which is why taking away the data is acceptable.

- operator==(Image&& other)—the move assignment operator Like the assignment operator, except that other is not const. Data is taken away from it. The compiler automatically uses this operation when it is sure that other will be destroyed soon.

In Listing 16.20, the compiler uses both to avoid copies:

- vector must first create an empty object with Image{} in push_back. Containers use this default creation without arguments when they need it. The newly created Image is then assigned using the move assignment operator.

- vector<Image> collection = ... is initialized with the move constructor. That means the return value, and thus result, takes the data instead of copying the entire object.

How do the two operations you just learned about this? The matter becomes clear when you consider the following facts:

- The compiler ensures that other is short-lived and will be destroyed soon anyway.

- Therefore, other no longer needs its data, and they can serve a better purpose—avoiding a copy of the data.

- The object that is supposed to receive the data is usually freshly created—almost empty.

- The receiving object is supposed to have its data overwritten; it no longer needs its old—mostly data.

- Both involved objects must be valid before the operation. this is at least initialized empty; other contains the valuable data.

- Both objects must be valid after the operation. this contains the data; other can be empty, ready for the destructor call.

If you had to implement the operations yourself with these requirements—which you don't have to, as the compiler does it—you could do it as in the following listing.

```cpp
// https://godbolt.org/aooW86vs8
#include <vector>
class Image {
    std::vector<std::byte> data_; // byte has been available
public:
    C++17
    explicit Image(const char* fn) { /*...*/ }
    Image(Image&& other) noexcept // move constructor
        : data_() // create empty
    {
        using std::swap;
        swap(data_, other.data_);
    }
    Image& operator=(Image&& other) noexcept { // move assignment
        using std::swap;
        swap(data_, other.data_);
        return *this;
    }
};
```

# **Listing 16.21** Implementation of the two move operations.

With swap, you exchange almost any element in the most efficient way imaginable. Normally, you can also directly use std::swap, but it has become an idiom that a prior using std::swap leaves the possibility open to use an even better swap variant. More important, however, is the question of what is being swapped here. Actually, everything has already been said with the preceding bulleted list: before swapping, other contains the data, afterward this does; before, this is (mostly) empty, afterward it is other. Assuming that swap does not copy any data, you have very effectively transferred the data from other to this and left both objects in a correct state.

The swap function is useful, but in some cases, the similar exchange function is more appropriate:

```cpp
Image(Image&& other) noexcept // move constructor
: data_(std::exchange(other.data_, {}))
{}
```

Effectively, r = exchange(old, new) performs r=old and old=new sequentially whenever possible, using move. Thus, you can usually initialize all members in the move constructor.

If you do not write a copy constructor, assignment operator, or destructor because you do not need them, then you usually do not need either of objects the move operations. In that case, the compiler generates the move operations for you.

Or the compiler prohibits moving, similar to how it would prohibit copying. For example, if you have a const data field, it cannot be moved from.

If you manage to create a movable data type, it is ideal for return values and for being put into standard containers. The compiler ensures that sorting, swapping, pushing, and resizing use the move operations.

## 16.9.1 What the Compiler Generates

It is important to understand when the compiler takes over the work of generating a constructor or operator= for programmers and when it does not. The rules are not trivial, but they are written in such a way that your program becomes as safe and fast as possible automatically.
