```
```cpp
Line line(10.0);

// get initially set length.
cout << "Length of line : " << line.getLength() <<endl;
// set line length again
line.setLength(6.0);
cout << "Length of line : " << line.getLength() <<endl;

return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```
Object is being created, length = 10

Length of line : 10

Length of line : 6
```
```

# Using Initialization Lists to Initialize Fields

In case of parameterized constructor, you can use following syntax to initialize the fields:

```
```cpp
Line::Line( double len): length(len)
{
    cout << "Object is being created, length = " << len << endl;
}
```
```

Above syntax is equal to the following syntax:

```
```cpp
Line::Line( double len)
{
    cout << "Object is being created, length = " << len << endl;
    length = len;
}
```
```

If for a class C, you have multiple fields X, Y, Z, etc., to be initialized, then use can use same syntax and separate the fields by comma as follows:

```
```cpp
C::C( double a, double b, double c): X(a), Y(b), Z(c)
{
```
```