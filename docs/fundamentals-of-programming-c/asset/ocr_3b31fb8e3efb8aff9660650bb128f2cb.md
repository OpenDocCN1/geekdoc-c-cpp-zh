thus evaluates to a reference to cout. This process of returning the object that was passed allows the <<
operator to be chained, as in

```
cout << x << y << endl;
```

This is the syntax for

```
operator<<(operator<<(operator(cout, x), y), endl);
```

If you examine this expression carefully, you will see that the first argument to the calls of operator<<
isim simply cout.

For our enhanced Point class, operator<< could look like:

```
ostream<<(ostream& os, const Point& pt) {
os os << '{' << pt.getX() << ', ' << pt.getY() << '}'
return os;
}
```

The function simply returns the same ostream object that was passed into the first param-\eter.
Given the above definitions of operator+ and operator<<, clients can write code such as

```
Point my_point(1, 2), your_point(0.45, 0);
cout << "Point 1: " << my_point << endl;
cout << "Point 2: " << my_point << endl;
cout << my_point << " + " << your_point
cout << " = " << my_point + your_point << endl;
```

which displays

```
Point 1: (1.0, 2.0)
Point 2: (0.45, 0.0)
(1.0, 2.0) + (0.45, 0.0) = (1.45, 2.0)
```

When developers provide such an operator<< function, clients can print objects just as easily
as printing the base data types.
The operator is not overloaded for the std::vector class, but we now easily do it ourselves
needed. For a vector of integers, the following function

```
ostream<<(ostream& os, const vector<int>& vec) {
os << '{';
int n = vec.size();
if (n != 0) {
for (int i = 1; i < n; i++)
os << << << ' << vec[i];
}
return os;
}
```