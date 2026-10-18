element. The value v.end() is a special value that serves as a sentinel value. It is not an ordinary iterator, but you can compare v.end() to an iterator using == and !=. The value v.end() is analogous to the value NULL used to mark the end of a linked list of the kind discussed in Chapter 13.

The following for loop from Display 18.1 uses this exact technique with the vector named container:

```
vector<int>::iterator p;
for (p = container.begin(); p != container.end(); p++)
    cout << *p << " ";
```

The action taken at the location of the iterator p is

```
cout << *p << " ";
```

The dereferencing operator * is overloaded for STL container iterators so that *p produces the element at location p. In particular, for a vector container, *p produces the element located at the iterator p. So, the cout statement above outputs the element located at the iterator p and the entire for loop outputs all the elements in the vector container.

The dereferencing operator *p always produces the element located at the iterator p. In some situations, *p produces read-only access, which does not allow you to change the element. In other situations, it gives you access to the element and will let you change the element. For vectors, *p will allow you to change the element located at p, as illustrated by the following for loop from Display 18.1:

```
for (p = container.begin(); p != container.end(); p++)
    *p = 0;
```

This for loop cycles through all the elements in the vector container and changes all the elements to 0.

# PROGRAMMING TIP Use auto to Simplify Variable Declarations

The auto keyword can make your code much more readable when it comes to templates and iterators. Declaring an iterator can be really verbose:

```
vector<int>::iterator p = v.begin();
```

We can do the same thing much more compactly with auto:

```
auto p = v.begin();
```

# PITFALL Compiler Problems

Some compilers have problems with iterator declarations. You can declare an iterator in different ways. For example, we have been using the following:

```
using std::vector;
...
vector<char>::iterator p;
```