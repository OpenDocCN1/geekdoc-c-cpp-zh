However, for what it does it closely resembles std::string (Chapter 36) and illustrates techniques used for the implementation of the standard-library string.

# 19.4 Friends

An ordinary member function declaration specifies three logically distinct things: [1] The function can access the private part of the class declaration.
[2] The function is in the scope of the class.
[3] The function must be invoked on an object (has a this pointer).

By declaring a member function static (§16.2.12), we can give it the first two properties only. By declaring a nonmember function a friend, we can give it the first property only. That is, a function declared friend is granted access to the implementation of a class just like a member function but is otherwise independent of that class.

For example, we could define an operator that multiplies a Matrix by a Vector. Naturally, Vector and Matrix hide their respective representations and provide a complete set of operations for manipulating objects of their type. However, our multiplication routine cannot be a member of both. Also, we don’t really want to provide low-level access functions to allow every user to both read and write the complete representation of both Matrix and Vector. To avoid this, we declare the operator* a friend of both:

```
constexpr rc_max {4}; // row and column size
class Matrix;

class Vector {
float v[rc_max];
// ...
friend Vector operator*(const Matrix&, const Vector&);
};
class Matrix {
Vector v[rc_max];
// ...
friend Vector operator*(const Matrix&, const Vector&);
};
```

Now operator*() can reach into the implementation of both Vector and Matrix. That would allow sophisticated implementation techniques, but a simple implementation would be:

```
Vector operator *(const Matrix& m, const Vector& v)
{
Vector r;
for (int i = 0; i!=rc_max; i++) { // r[i] = m[i] * v;
r.v[i] = 0;
for (int j = 0; j!=rc_max; j++)
r.v[i] += m.v[i].v[j] * v.v[j];
}
return r;
```