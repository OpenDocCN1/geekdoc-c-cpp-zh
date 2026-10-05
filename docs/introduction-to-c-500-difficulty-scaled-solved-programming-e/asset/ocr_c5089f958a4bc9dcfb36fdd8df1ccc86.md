```
template <typename T> class Circle
{
private:
  T rad;
public:
  Circle<T>(T r = 0) rad = r;
  void operator+(T i) { rad += i; }
  Circle<T> operator+(const Circle<T>& c) const;
  template <typename V> friend ostream& operator<<(ostream& out, const Circle<V>& c);
};
```

```
template <typename T> Circle<T> Circle::operator+(const Circle<T>& c) const
{
  Circle<T> tmp;
  tmp.rad = rad + c.rad;
  return tmp;
}
```

```
template <typename V> ostream& operator<<(ostream& out, const Circle<V>& c)
{
  out << c.rad << '\n';
  return out;
}
```

**Comments:** From the given code we understand that we need to overload operators. We also define a template function that can be used by all versions of the class.

**C.23.4** Define the Map_Key<T1, T2> class with two private members of type T1 and T2. Add appropriate functions in the class so that the following program works.

```
template <typename T1, typename T2> class Map_Key
private:
  T1 key;
  T2 val;
public:
  ?? check(???) /* Define the check() which takes parameter a value (e.g., k) and checks if the value of the key is the same as k. */
  ?? get(???) /* Define the get() so that it returns the value. */
  // Add any other function you think is needed.)
```

```
int main()
{
  Map_Key<string, int> mk_1("One", 1), mk_2("Two", 2);
  Map_Key<string, int> mk_3 = mk_1 + mk_2;
  /* Declare a vector (e.g., v) of type Map_Key and store mk_1, mk_2, and mk_3 in it. Then, read a string and check if is stored in v. If it is, the program should display the value of check. For example, if the user enters One, the program should display 1. */
  ...
```