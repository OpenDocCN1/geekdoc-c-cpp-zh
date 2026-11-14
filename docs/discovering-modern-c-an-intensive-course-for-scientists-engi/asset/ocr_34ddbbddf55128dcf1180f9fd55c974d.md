# 3.3.1 A Container Example

Let us, for example, write a generic vector class, in the sense of linear algebra not like an STL vector. First, we implement a class with the most of fundamental operators only:

# Listing 3-1: Template vector class

```
template <typename T>
class vector
{
public:
    explicit vector(int size)
    : my_size(size), data( new T[my_size] )
    {
    }

    vector(const vector& that)
    : my_size(that.my_size), data(new T[my_size])
    {
        std::copy(&that.data[0], &that.data[that.my_size], &data[0]);
    }

    int size() const { return my_size; }

    const T& operator[](int i) const
    {
        check_index(i);
        return data[i];
    }
    // ...

private:
    int my_size;
    std::unique_ptr<T[]> data;
};
```

The template class is not essentially different from a non-template class. There is only the extra parameter T as a placeholder for the type of its elements. We have member variables like my_size and member functions like size() that are not affected by the template parameter. Other functions like the bracket operator or the copy constructor are parameterized, still resembling their non-template equivalent: wherever we had double before, we put the type parameter T as for return types or in allocations. Likewise, the member variable data is just parameterized by T.

Template parameters can be defaulted. Assume that our vector class parameterizes not only the value type, but also orientation and location:

```
struct row_major (); // just for tagging
struct col_major (); // ditto
struct heap ();
```