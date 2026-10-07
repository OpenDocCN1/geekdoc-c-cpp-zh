The auto keyword can simplify template declarations. For example, if il is an object of type std::initializer_list<double>, you can replace

```
for (std::initializer_list<double>::iterator p = il.begin();
p!=il.end(); p++)
```

with this:

```
for (auto p = il.begin()); p!=il.end(); p++)
```

# decltype

The decltype keyword creates a variable of the type indicated by expression. The following statement means "make the same type as x," where x is an expression:

Here are a couple of examples:

```
double x;
int n;
decltype(x*n) q; // q same type as x*n, i.e., double
decltype(&x) pd; // pd same as &x, i.e., double *
```

This is particularly useful in template definitions, when the type may not be determined until a specific instantiation is made:

```
template<typename T, typename U>
void ef(T t, U u)
{
decltype(T*U) tu;
}
```

Here, tu is of whatever type results from the operation T*U, assuming operation is defined. For example, if T is char and U is short, tu would be of type int because of the integer promotions that take place in integer arithmetic.

The workings of decltype are more complicated than those of auto, and the resulting types can be references or be const-qualified, depending on the expressions used. Here are some examples:

```
int j = 3;
int &k = j;
const int &n = j;
decltype(n) il; // il type const int &
decltype(j) i2; // i2 type int
decltype((j)) i3; // i3 type int &
ndecltype(k + 1) i4; // i4 type int
```

See Chapter 8, "Adventures in Functions," for the rules that lead to these results.