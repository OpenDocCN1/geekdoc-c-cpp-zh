The value being returned is not force1, which should be left unaltered by the process, nor force2, which should also be unaltered. Thus the return value can’t be a reference to an object that is already present in the calling function. Instead, the sum is a new, temporary object computed in Vector::operator+(), and the function shouldn’t return a reference to a temporary object either. Instead, it should return an actual vector object, not a reference:

```
```cpp
Vector Vector::operator+(const Vector & b) const
{
    return Vector(x + b.x, y + b.y);
}
```
```

There is the added expense of calling the copy constructor to create the returned object, but that is unavoidable.

One more observation: In the Vector::operator+() example, the constructor call Vector(x + b.x, y + b.y) creates an object that is accessible to the operator+() method; the implicit call to the copy constructor produced by the return statement, however, creates an object that is accessible to the calling program.

# ## Returning a const Object

The preceding definition of Vector::operator+() has a bizarre property. The intended use is this:

```
```cpp
net = force1 + force2;                                      // 1: three Vector objects
```
```

However, the definition also allows you to use the following:

```
```cpp
force1 + force2 = net;                                      // 2: dysleptic programming
cout << (force1 + force2 = net).magval() << endl;           // 3: demented programming
```
```

Three questions immediately arise: Why would anyone write such statements? Why are they possible? What do they do?

First, there is no sensible reason for writing such code, but not all code is written for sensible reasons. People, even programmers, make mistakes. For instance, if the comparison operator==() were defined for the Vector class, you might mistakenly type

```
```cpp
if (force1 + force2 = net)
```
```

instead of this:

```
```cpp
if (force1 + force2 == net)
```
```

Also programmers tend to be ingenious, and this can lead to ingeniously adventurous mistakes.

Second, this code is possible because the copy constructor constructs a temporary object to represent the return value. So in the preceding code, the expression force1 + force2 stands for that temporary object. In Statement 1, the temporary object is assigned to net. In Statements 2 and 3, net is assigned to the temporary object.