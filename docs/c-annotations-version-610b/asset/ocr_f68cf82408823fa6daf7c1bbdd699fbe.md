# 18.4.6 Using ‘shared_ptr’ objects for arrays (C++11)

Different from the `unique_ptr` class no specialization exists for the `shared_ptr` class to handle dynamically allocated arrays of objects.

But like `unique_ptr`s, with `shared_ptr`s referring to arrays the dereferencing operator makes little sense while in these circumstances `shared_ptr` objects would benefit from index operators.

It is not difficult to create a class `shared_array` offering such facilities. The class template `shared_array`, derived from `shared_ptr` merely should provide an appropriate `deleter` to make sure that the array and its elements are properly destroyed. In addition it should define the index operator and optionally could declare the dereferencing operators using delete.

Here is an example showing how `shared_array` can be defined and used:

```
```cpp
struct X
{
    ~X()
    {
        cout << "destr\n";  // show the object's destruction
    }
};
template <typename Type>
class shared_array: public shared_ptr<Type>
{
    struct Deleter             // Deleter receives the pointer
    {                          // and calls delete[]
        void operator()(Type* ptr)
        {
            delete[] ptr;
        }
    };
public:
    shared_array(Type *p)                 // other constructors
    :                                      // not shown here
        shared_ptr<Type>(p, Deleter())
    {}
    Type &operator[](size_t idx)    // index operators
    {
        return shared_ptr<Type>::get()[idx];
    }
    Type const &operator[](size_t idx) const
    {
        return shared_ptr<Type>::get()[idx];
    }
    Type &operator*() = delete;     // delete pointless members
    Type const &operator*() const = delete;
    Type *operator->() = delete;
    Type const *operator->() const = delete;
};
int main()
{
    shared_array<X> sp(new X[3]);
    sp[0] = sp[1];
}
```
```