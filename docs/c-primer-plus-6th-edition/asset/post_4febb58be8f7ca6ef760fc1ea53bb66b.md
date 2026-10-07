
# Chapter 12 Classes and Dynamic Memory Allocation

```cpp
String & String::operator=(const String & st)
{
    if (this == &st) // object assigned to itself
        return *this; // all done
    delete [] str; // free old string
    len = str.len;
    str = new char[len + 1]; // get space for new string
    std::strcpy(str, st.str); // copy the string
    return *this; // return reference to invoking object
}
```

In particular, the method should check for self-assignment; it should free memory pointed to by the member pointer; it should copy the data, not just the address of the data; and it should return a reference to the invoking object.

# Don's and Dos

The following excerpt contains two examples of what not to do and one example of a good constructor:

```cpp
String::String()
{
    str = "default string"; // oops, no new []
    len = std::strlen(str);
}
```

```cpp
String::String(const char * s)
{
    len = std::strlen(s);
    str = new char; // oops, no []
    std::strcpy(str, s); // oops, no room
}
```

```cpp
String::String(const String & st)
{
    len = st.len;
    str = new char[len + 1]; // good, allocate space
    std::strcpy(str, st.str); // good, copy value
}
```

The first constructor fails to initialize str. The destructor, when called for a default object, applies delete to str. Result of applying delete to a pointer initialized by str is undefined, and it is probably bad. Any of the following would be:

```cpp
String::String()
{
    len = 0;
    str = new char[1]; // uses new with []
    str[0] = '\0';
}
```

# Things to Remember When Using new in Constructors 661

```cpp
String::String()
{
  len = 0; // or, with C++11, str = nullptr;
}
```

```cpp
String::String()
{
  static const char * s = "C++"; // initialized just once
  len = std::strlen(str);
  str = new char[len + 1]; // uses new with []
  std::strcpy(str, s);
}
```

Next, the second constructor in the original excerpt applies new, but it fails to request the correct amount of memory; hence new returns a block containing space for just one character. Attempting to copy a longer string to that location is asking for memory problems. Also use of new without brackets is inconsistent with the correct form of the other constructors.

The third constructor is fine.

Finally, here's a destructor that doesn't work correctly with the previous constructors:

```cpp
String::~String()
{
  delete str; // oops, should delete [] str;
}
```

The destructor uses delete incorrectly. Because the constructors request arrays of characters, the destructor should delete an array.

# Memberwise Copying for Classes with Class Members

Suppose you use the String class, or, for matter, the standard string class as a type for class members:

```cpp
class Magazine
{
private:
  String title;
  string publisher;

};
```

String and string both use dynamic memory allocation. Does that mean you need to write a copy constructor and assignment operator for the Magazine class? No—at least in itself. The default memberwise copying and assignment behavior does have some smarts. If you copy or assign one Magazine object to another, memberwise copying uses the copy constructors and assignment operators defined for the member types. That is, the

# Chapter 12 Classes and Dynamic Memory Allocation

String copy constructor will be used to copy the title member object to another, the String assignment operator will be used to assign the title member of one Magazine object to another, and so on. Things get more complicated, however, if the Magazine class needs a copy constructor and assignment operator for other class member. In that case, those functions have to call the String and string copy constructors and assignment operators explicitly. But that's a tale of Chapter 13, "Class Inheritance."

# Observations About Returning Objects

When a member or standalone function returns an object, you have choices. The function could return a reference to an object, a constant reference to an object, an object, or a constant object. By now, you've seen examples of all the last, so it's a good time to review your options.

# Returning a Reference to a const Object

The usual reason for using a const reference is efficiency, but there are restrictions on when this can be used. If a function returns an object that is passed to it, either by object invocation or as an argument, you can increase the efficiency of the method by having it return a reference. For example, you wanted to write a function Max() that returns the larger of two objects, where Vector is the class developed in Chapter 11. The function would be used in this manner:

```cpp
Vector force1(50,60);
Vector force2(10,70);
Vector max;
max = Max(force1, force2);
```

Either of the following implementations work:

```cpp
// version 1
Vector Max(const Vector &v1, const Vector &v2)
{
  if (v1.len() > v2.len())
    return v1;
  else
    return v2;
}
```

```cpp
// version 2
const Vector &Max(const Vector &v1, const Vector &v2)
{
  if (v1.len() > v2.len())
    return v1;
  else
    return v2;
}
```

# Observations About Returning Objects

There are three important points here. First, recall that returning an object invokes the copy constructor, whereas returning a reference doesn't. Version 2 does less work and is more efficient. Second, the reference to an object exists when the calling function is executing. In this example, the reference is to either force1 or force2, and both objects are defined in the calling function, so this requirement is met. Third, both v1 and v2 are declared as const, so the return type has to match.

# Returning a Reference to a Nonconst Object

Two common examples of returning a non-const object are overloading the assignment operator and overloading the << operator for cout. The first is done for reasons of efficiency, and the second for reasons of necessity. The return value of operator= is used for chained assignment:

```cpp
String s1("Good stuff");
String s2, s3;
s3 = s2 = s1;
```

In this code, the return value of operator=(s1) is assigned to s3. Returning a String object or a reference to a String object would work, but with the Vector example, using a reference allows to avoid calling the String constructor. In this case, the return is not const because the operator returns a reference to s2, which it modifies.

The return value of operator<< is used for chained output:

```cpp
String s1("Good stuff");
cout << s1 << "is coming!";
```

The return value of operator<<(cout, s1) becomes the object to display the string "is coming!". Here, the return type has to be ostream and not just ostream. Using an ostream return type would require calling the ostream copy constructor, and as it turns out, the ostream class does not have a public copy constructor. Fortunately, returning a reference to cout poses no problems because cout is already in scope in the calling function.

# Returning an Object

If the object being returned is local to the called function, then it should not be returned by reference because the local object has its destructor called when the function terminates. Thus, when control returns to the calling function, there is no object left for the reference to refer. In these circumstances, you should return an object, not a reference. Typically, overloaded arithmetic operators fall into this category. Consider this example, which uses the Vector class:

```cpp
Vector force1(50,60);
Vector force2(10,70);
Vector net;
net = force1 + force2;
```

# Chapter 12 Classes and Dynamic Memory Allocation

The value being returned is not force, which should be left unaltered by the process, nor force2, which should also be unaltered. Thus the return value can't be a reference to an object that is already present in the calling function. Instead, the sum is a new, temporary computed object in Vector::operator(), and the function shouldn't return a reference to a temporary object either. Instead, it should return an actual vector object, not a reference:

```cpp
Vector::operator+(const Vector & b) const
{
    return Vector(x + b.x, y + b.y);
}
```

There is the added effect of calling the copy constructor to create the returned object, but that is unavoidable.
One observation: In the Vector::operator+() example, the constructor call Vector(x + b.x, y + b.y) creates an object that is accessible to the operator+() method; the implicit call to the copy constructor for the object produced by the return statement, however, creates an object that is accessible to the calling program.

# Returning a const Object

The preceding definition of Vector::operator+() has a bizarre property. The intended use is this:

```cpp
net = force1 + force2; // 1: three Vector objects
```

However, the definition also allows you to use the following:
force + force2 = net; // 2: dyslexic programming
cout << (force + force2 = net).len() << endl; // 3: demented programming

Three questions immediately arise. Why would anyone write such code? Why are they possible? What do they do?
First, there is no sensible reason for writing such code, but not all is written for sensible reasons. People, even programmers, make mistakes. For instance, if the comparison operator== is defined for the Vector class, one might mistakenly type

```
if (force + force2 = net)
```

instead of:
if (force + force2 == net)

Also programmers tend to be ingenious, and this can lead to ingeniously adventurous mistakes.
Second, the code is possible because the copy constructor constructs a temporary object to represent the return value. So in the preceding code, the expression force1 + force2 stands for that temporary object. In Statement 1, the temporary object is assigned to net. In Statements 2 and 3, net is assigned to the temporary object.
