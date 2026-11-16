which displays

```
Point 1: (1.0, 2.0)
Point 2: (0.45, 0.6)
(1.0, 2.0) + (0.45, 0.6) = (1.45, 2.0)
```

When class developers provide such an operator<< function, clients can print out objects just as easily as printing the basic data types.

The << operator is not overloaded for the std::vector class, but we now easily can do it ourselves as needed. For a vector of integers, the following function

```
ostream& operator<<(ostream& os, const std::vector<int>& vec) {
 os << '{';
 int n = vec.size();
 if (n != 0) {
 os << vec[0]
 for (int i = 1; i < n; i++)
 os << ',' << vec[i];
 }
 os << '}';
 return os;
}
```

provides the necessary functionality. Given this operator<< function, clients can display vectors as they would a built in type:

```
std::vector<int> list(10, 5);
std::cout << list << '\n';
```

This code fragment prints

```
{(5,5,5,5,5,5,5,5,5,5)}
```

# 15.7.2 Operator Methods

A class may define operator methods. A method for a unary operator accepts no parameters, and a method for a binary operator accepts only one parameter. The "missing" parameter is the object upon which the operator is applied; that is, the this pointer. To see how operator methods work, consider an enhanced rational class:

```
class EnhancedRational {
 int numerator;
 int denominator;
 public:
 /* Other details omitted */
 // Unary plus returns the double-precision floating-point
 // equivalent of the rational number.
 double operator+() const {
 return static_cast<double>(numerator)/denominator;
 }
```