# Chapter 12 Classes and Dynamic Memory Allocation

The value being returned is not force, which should be left unaltered by the process, nor force2, which should also be unaltered. Thus the return value can't be a reference to an object that is already present in the calling function. Instead, the sum is a new, temporary computed object in Vector::operator+(), and the function shouldn't return a reference to a temporary object either. Instead, it should return an actual vector object, not a reference:

```
Vector::operator+(const Vector & b) const
{
    return Vector(x + b.x, y + b.y);
}
```

There is the added effect of calling the copy constructor to create the returned object, but that is unavoidable.
One observation: In the Vector::operator+() example, the constructor call Vector(x + b.x, y + b.y) creates an object that is accessible to the operator+() method; the implicit call to the copy constructor for the object produced by the return statement, however, creates an object that is accessible to the calling program.

# Returning a const Object

The preceding definition of Vector::operator+() has a bizarre property. The intended use is this:

```
net = forcel + force2; // 1: three Vector objects
```

However, the definition also allows you to use the following:
force + force2 = net; // 2: dyslexic programming
cout << (force + force2 = net).magval() << endl; // 3: demented programming

Three questions immediately arise. Why would anyone write such code? Why are they possible? What do they do?
First, there is no sensible reason for writing such code, but not all is written for sensible reasons. People, even programmers, make mistakes. For instance, if the comparison operator== is defined for the Vector class, one might mistakenly type

```
if (force + force2 = net)
```

instead of:
if (force + force2 == net)

Also programmers tend to be ingenious, and this can lead to ingeniously adventurous mistakes.
Second, the code is possible because the copy constructor constructs a temporary object to represent the return value. So in the preceding code, the expression forcel + force2 stands for that temporary object. In Statement 1, the temporary object is assigned to net. In Statements 2 and 3, net is assigned to the temporary object.