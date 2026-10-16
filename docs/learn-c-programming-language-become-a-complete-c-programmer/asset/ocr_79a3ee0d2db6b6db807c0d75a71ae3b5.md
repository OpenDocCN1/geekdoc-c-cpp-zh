created object is usually a very bad idea: using a pointer gives notational problems, and referring to an object on the free store (whether by a pointer or by a reference) results in memory management problems. Instead, return objects by value. For large objects, such as a Matrix, define move operations to make such transfers of values efficient (§3.3.2, §17.5.2). For example:

```
Matrix operator+(const Matrix& a, const Matrix& b) // return-by-value
{
Matrix res {a};
return res+=b;
}
```

Note that operators that return one of their argument objects can – and usually do – return a reference. For example, we could define Matrix’s operator += like this:

```
Matrix& Matrix::operator+=(const Matrix& a) // return-by-reference
{
if (dim[0]!=a.dim[0] || dim[1]!=a.dim[1])
throw std::exception("bad Matrix += argument");

double * p = elem;
double* q = a.elem;
double* end = p+dim[0]*dim[1]; while(p!=end)

*p++ += *q++
return *this;
}
```

This is particularly common for operator functions that are implemented as members. If a function simply passes an object to another function, an rvalue reference argument should be used (§17.4.3, §23.5.2.1, §28.6.3).

# 18.2.5 Operators in Namespaces

An operator is either a member of a class or defined in some namespace (possibly the global namespace). Consider this simplified version of string I/O from the standard library:

```
namespace std { // simplified std
class string {
//...
};
class ostream {
//...
ostream& operator<<(const char*); // output C-style string
};

extern ostream cout;
ostream& operator<<(ostream&, const string&); // output std::string }// namespace std
int main() {
```