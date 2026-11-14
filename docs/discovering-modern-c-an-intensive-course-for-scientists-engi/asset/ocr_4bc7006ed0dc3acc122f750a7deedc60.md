Imagine the previous expression without ADL:

```
```
A = rocketscience::operator+(rocketscience::operator+(B, C), D);
```
```

Similarly ugly and even more cumbersome is streaming I/O when the namespace must be qualified. Since user code should not be in namespace std::;, the operator<< for a class is preferably defined in that class's namespace. This allows ADL to find the right overload for each type, e.g.:

```
```
std::cout << A << E << B << F << std::endl;
```
```

Without ADL we would need to qualify the namespace of each operator in its verbose notation. This would turn the previous expression into

```
```
std::operator<<(chez_herbert::operator<<(
    rocketscience::operator<<(chez_herbert::operator<<(
        rocketscience::operator<<(std::cout, A), E), B),
    F), std::endl);
```
```

The ADL mechanism can also be used to select the right function template overload when the classes are distributed over multiple namespaces. The L1 norm from linear algebra is defined for both matrices and vectors, and we want to provide a template implementation for both:

```
```
template <typename Matrix>
double one_norm(const Matrix& A) { ... }
```
```

```
```
template <typename Vector>
double one_norm(const Vector& x) { ... }
```
```

How can the compiler know which overload we want? One possible solution is to introduce a namespace for matrices and one for vectors so that the correct overload can be selected by ADL:

```
```
namespace rocketscience {
    namespace mat {
        struct sparse_matrix {};
        struct dense_matrix {};
        struct uber_matrix^; // Sadly, 0 is not allowed in C++
        template <typename Matrix>
        double one_norm(const Matrix& A) { ... }
    }
    namespace vec {
        struct sparse_vector {};
        struct dense_vector {};
        struct uber_vector {};
        template <typename Vector>
```
```

5. Of course, we use the original German spelling of über--sometimes even seen in American papers. Please note that special characters like ä are not allowed in names.