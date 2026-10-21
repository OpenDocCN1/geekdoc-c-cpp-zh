As a consequence of the corresponding wording in the standard, we have to ensure that the return value of placement new is always used with each access to the memory if the objects there have constant or reference members:

```
struct X {
    const int n;
    double d;
};
X* p = new X{7, 8.8};
p = new (p) X{42, 9.9};  // Note: assign return value of placement new to p
int i = p->n;           // OK, i is guaranteed to be 42
auto d = p->d;          // OK, d is guaranteed to be 9.9
```

Unfortunately, this rule is not widely known and used. Even worse, in practice, you cannot always easily use the return value of placement new. You might need additional objects, and the current allocator interface does not support this.

One example where using the return value causes overhead is when the storage is an existing member.

That would be the case for std::optional and std::variant.

Here is a simplified example of implementing something like std::optional:

```
template<typename T>
class optional
{
private:
    T payload;
public:
    optional(const T& t)
    : payload(t) {}

    template<typename... Args>
    void emplace(Args&&... args) {
        payload.~T();
        ::new (&payload) T(std::forward<Args>(args)...); // *
    }

    const T& operator*() const & {
        return payload;  // OOPS: returns payload not reinitialized
    }
};
```

If here, T is a structure with constant or reference members:

```
struct X {
    const int _i;
    X(int i) : _i(i) {}
}
friend std::ostream& operator<< (std::ostream& os, const X& x) {
    return os << x._i;
```