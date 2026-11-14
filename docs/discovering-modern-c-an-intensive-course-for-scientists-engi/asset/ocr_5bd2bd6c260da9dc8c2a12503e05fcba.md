It defines a type only when the condition holds. Our realization is compatible with <type_traits> from C++11. The program snippet here serves as illustration while we use the standard meta-function in production software.

As in C++14, we want to add a template alias for making the notation more concise:

```
```cpp
template <bool Cond, typename T = void>
using enable_if_t = typename enable_if<Cond, T>::type;
```
```

As before, it saves us from writing the typename::type pair. Now we have all we need to implement the L1 norm in the generic fashion we aimed for:

```
```cpp
1 template <typename T>
2 enable_if_t<is_matrix<T>::value, Magnitude_t<T>>
3 inline one_norm(const T& A)
4 {
5 using std::abs;
6 Magnitude_t<T> max(0);
7 for (unsigned c = 0; c < num_cols(A); c++) {
8 Magnitude_t<T> sum(0);
9 for (unsigned r = 0; r < num_cols(A); r++)
10 sum += abs(A[r][c]);
11 max = max < sum ? sum : max;
12 }
13 return max;
14 }
```
```

```
```cpp
16 template <typename T>
17 enable_if_t<is_vector<T>::value, Magnitude_t<T>>
18 inline one_norm(const T& v)
19 {
20 using std::abs;
21 Magnitude_t<T> sum(0);
22 for (unsigned r = 0; r < size(v); r++)
23 sum += abs(v[r]);
24 return sum;
25 }
```
```

The selection is now driven by enable_if in lines 2 and 17. Let us look at line 2 in detail for a matrix argument:

+   1. is_matrix<T> is evaluated to (i.e., inherited from) true_type.
+   2. enable_if_t<> becomes Magnitude_t<T>.
+   3. This is the return type of the function overload.

Here is what happens in this line when the argument is not a matrix type.

+   1. is_matrix<T> is evaluated to false_type.
+   2. enable_if_t<> cannot be substituted because enable_if<>::type does not exist in this case.