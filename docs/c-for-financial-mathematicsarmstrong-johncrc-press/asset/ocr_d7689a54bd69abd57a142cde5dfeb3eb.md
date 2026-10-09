```
private:

T* data;
/* Rule of three - we make these private */
SimpleVector(const SimpleVector& o);
SimpleVector& operator=(const SimpleVector& o);
};
```

We have provided inline implementations of all methods except the constructor of our SimpleVector.

As with template functions, all definitions should be provided alongside the declarations in header files. Unfortunately you need to repeat the line declaring the template parameters you are using for every function definition. In addition you must include the template parameter in the qualifier of the name for all the functions you define. For example, here is how we have defined the constructor for SimpleVector.

```
template <typename T>
SimpleVector<T>::SimpleVector( int size ) {
data = new T[size];
}
```

As demonstrated in the unit test below, we can now use SimpleVector to store various different data types.

```
void testSimpleVector() {
SimpleVector<double> v1(3);
v1.set(1, 2.0);
ASSERT(v1.get(1) == 2.0);

SimpleVector<int> v2(3);
v2.set(1, 2);
ASSERT(v2.get(1) == 2);

SimpleVector<string> v3(3);
v3.set(1, "Test string");
ASSERT(v3.get(1) == "Test string");
}
```

It is possible to use multiple parameters in your templates. It is also possible to use certain simple data types such as constant integers as template parameters. One example of this is the type array from the library <array>, which is like a vector but of fixed length. When you create instances of array you must specify both the type of the data and the length. Here is an example of how you can use this type.

```
void testArray() {
```