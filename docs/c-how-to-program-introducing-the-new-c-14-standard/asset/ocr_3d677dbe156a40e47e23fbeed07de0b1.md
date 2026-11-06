# Overloaded Subscript Operators

Lines 27 and 30 of **Fig. 10.10** declare two overloaded subscript operators (defined in **Fig. 10.11** in lines 73–80 and 84–91, respectively). When the compiler sees the expression `integers1[5]` (**Fig. 10.9**, line 56), it invokes the appropriate overloaded `operator[]` member function by generating the call

```
```cpp
integers1.operator[](5)
```
```

The compiler creates a call to the `const` version of `operator[]` (**Fig. 10.11**, lines 84–91) when the subscript operator is used on a `const` `Array` object. For example, if you pass an `Array` to a function that receives the `Array` as a `const Array&` named `z`, then the `const` version of `operator[]` is required to execute a statement such as

```
```cpp
cout << z[3] << endl;
```
```

Remember, a program can invoke only the `const` member functions of a `const` object.