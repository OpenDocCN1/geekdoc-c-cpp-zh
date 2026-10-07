
## Chapter 12 Classes and Dynamic Memory Allocation

- An assignment operator if you don't define one
- An address operator if you don't define one

More precisely, the compiler generates definitions for the last three items if a program uses objects in such a way as to require them. For example, if you assign object to another, the program provides a definition for the assignment operator.

It turns out that the implicit copy constructor and the implicit assignment operator cause the String class problems.

The implicit address operator returns the address of the invoking object (that, is, the value of this pointer). That's fine for our purposes, and we won't discuss this member function further. The default destructor does nothing, and we won't discuss it either, other than to point out that the class has already provided a substitute for it. But the others do warrant discussion.

C++11 provides two special member functions—the move constructor and the move assignment operator. Chapter 18, "Visiting with the New C++ Standard," discusses these further.

# Default Constructors

If you fail to provide any constructors at all, C++ provides you with a default constructor. For example, you define a Klunk class and omit any constructors. In this case, the compiler supplies the following default:

```
Klunk::Klunk() {} // implicit default constructor
```

That is, it supplies a constructor (the *default* default constructor) that takes no arguments and does what needs. It's needed because creating an object always invokes a constructor:

```
Klunk klunk; // invokes default constructor
```

The default constructor makes klunk like an ordinary atomic variable; that is, its value at initialization is unknown.

After you define any constructor, C++ doesn't bother to define a default constructor. If you want to create objects that aren't initialized explicitly, you then have to define a default constructor explicitly. It's a constructor with no arguments, but you can use it to set particular values:

```
Klunk::Klunk() // explicit default constructor
{
  klunk_ct = 0;
}
```

A constructor with arguments still can be a default constructor if all its arguments are default values. For example, the Klunk class could have the following inline constructor:

```cpp
Klunk(int n = 0) { klunk_ct = n; }
```

# Dynamic Memory and Classes 639

However, you can have only one default constructor. That is, you cannot do this:

```
Klunk() { klunk_ct = 0 } // constructor #1
Klunk(int n = 0) { klunk_ct = n; } // ambiguous constructor #2
```

Why is this ambiguous? Consider the following two declarations:

```
Klunk kar(10); // clearly matches Klunk(int n)
Klunk bus;     // could match constructor
```

The second declaration matches constructor #1 (no argument), but it also matches constructor #2 (using the default argument 0). This will cause the compiler to issue an error message.

# Copy Constructors

A copy constructor is used to copy an object to a newly created object. That is, it's used during initialization, including passing functions by value and not during assignment. A copy constructor for a class normally has its prototype:

```
Class_name(const Class_name &);
```

Note that it takes a reference to a class object as its argument. For example, a copy constructor for the String class would have its prototype:

```
String(const String &);
```

You must know two things about a copy constructor: when it's used and what it does.

# When a Copy Constructor Is Used

A copy constructor is invoked whenever a new object is created and initialized to an existing object of the same kind. This happens in several situations. The most obvious situation is when you explicitly initialize a new object to an existing object. For example, given that motto is a String object, the following declarations invoke a copy constructor:

```
String detto(motto);               // calls String(const String &)
String metodo = motto;            // calls String(const String &)
String bad also = String(motto); // calls String(const String &)
String * pStringBad = new StringBad(motto);// calls String(const String &)
```

Depending on the implementation, the little declarations may use a copy constructor to create motto and also, or they may use a copy constructor to generate temporary objects whose contents are then assigned to metodo and also. The last example initializes an anonymous object to motto and assigns the address of the new object to the pstring pointer.

Less obvious, a compiler uses a copy constructor whenever a program generates copies of an object. In particular, it's used when a function passes an object by value (as callme2() does in Listing 12.3) or when a function returns an object. Remember,

by value means creating a copy of the original variable. A compiler also uses a copy constructor whenever it generates temporary objects. For example, a compiler might generate a temporary Vector object to hold an intermediate result when adding three Vector objects. Compilers vary as when they generate temporary objects, but all invoke a copy constructor when passing objects by value and returning them. In particular, this function in Listing 12.3 uses a copy constructor:

```
callme2(headline2);
```

The program uses a copy constructor to initialize sb, the formal StringBad-type parameter for the callme2() function.

By the way, fact that passing an object by value involves invoking a copy constructor is a good reason for passing by reference instead. That saves the time of invoking the constructor and

# What a Default Constructor Does

The default constructor performs memberwise copy. That is, it copies the value of each member of the object to the new object. This is also called shallow copying. In the case of Listing 12.3, the effect is that:

```
StringBad = sports;
```

This does not copy the string; it copies the pointer to the string. That is, after sailor is initialized to str, you wind up with two pointers to the same string. Figure 12.2 illustrates the problem of memberwise copying. The default destructor frees the memory pointed to by str. So the effect of destroying sailor is:

```
delete [] sailor.str;
```

Here, sports.str points to the same memory location that has already been freed by the destructor for sailor, and this is undefined, potentially harmful, behavior. In the case of Listing 12.3, the program produces mangled strings, which is usually a sign of memory misgement. Another disturbing symptom is attempting to delete the same memory twice can cause the program to abort. Microsoft Visual C++ 2010 (debug mode), for example, displays an error window "Debug Assertion Failed!", and g++ 4.4.1 on Linux reports "double free or corruption" and others. Others might provide different messages or no message, but the same evil lurks within the programs

# Fixing the Problem by Defining an Explicit Copy Constructor

The cure for the problems in the class design is to make a deep copy. That is, rather than just copying the address of the string, the copy constructor should duplicate the string and assign the duplicate to the str member. That way, each object gets its own string rather than referring to another object's string. And each of the destructor frees a different string rather than making attempts at freeing the same string. Here's how you can code StringBad::StringBad(const String& str)

```
{
    num_strings++; // handle static member update
    len = str.len; // same length
    str = new char[len + 1]; // allot space
    std::strcpy(str, str.str); // copy string to new location
}
```
