Conversion operators tend to be defined so that they can be used everywhere. However, it is possible to declare a conversion operator explicit and have it apply only for direct initialization (§16.2.6), where an equivalent explicit constructor would have been used. For example, the standard-library unique_ptr (§5.2.1, §34.3.1) has an explicit conversion to bool:

```
template <typename T, typename D = default_delete<T>>
class unique_ptr {
public:
// ...
explicit operator bool() const noexcept; // does *this hold a pointer (that is not nullptr)?
// ...
};
```

The reason to declare this conversion operator explicit is to avoid its use in surprising contexts. Consider:

```
void use(unique_ptr<Record> p, unique_ptr<int> q)
{
if (!p) // OK: wewant this use throw Invalid_uninque_ptr{};
bool b = p; // error ; suspicious use
int x = p+q; // error ;wedefinitely don’t want this
}
```

Had unique_ptr’s conversion to bool not been explicit, the last two definitions would have compiled. The value of b would have become true and the value of x would have become 1 or 2 (depending on whether q was valid or not).

# 18.4.3 Ambiguities

An assignment of a value of type V to an object of class X is legal if there is an assignment operator X::operator=(Z) so that V is Z or there is a unique conversion of V to Z. Initialization is treated equivalently.

In some cases, a value of the desired type can be constructed by repeated use of constructors or conversion operators. This must be handled by explicit conversions; only one level of user-defined implicit conversion is legal. In some cases, a value of the desired type can be constructed in more than one way; such cases are illegal. For example:

```
class X { /*...*/ X(int); X(const char*); };
class Y { /*...*/ Y(int); };
class Z { /*...*/ Z(X); };

X f(X); Y f(Y);
Z g(Z);

void k1() {
f(1); // error :ambiguous f(X(1)) or f(Y(1))? f(X{1}); // OK
f(Y{1}); // OK
```