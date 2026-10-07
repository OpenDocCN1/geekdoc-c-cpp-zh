# Chapter 15 Friends, Exceptions, and More

```
High * pb = static_cast<High *>(&blow); // valid upcast
Low * pl = static_cast<Low *>(&bar); // valid downcast
Pond * pmer = static_cast<Pond *>(&blow); // invalid, Pond unrelated
```

The first conversion is valid because an upcast can be explicit. The second conversion, from a base-class pointer to a derived-class pointer, can't be without an explicit conversion. But because the type cast in the other can be made without a type cast, it's valid to use static_cast for a downcast.

Similarly, an enumeration value can be converted to an integral type without a type cast, an integral type can be converted to an enumeration value with static_cast. You can also use static_cast to convert double to int, to float to long, and to perform the other numeric conversions.

The reinterpret_cast operator is inherently risky type casts. It doesn't let you cast away const, but it allows other unsafe things. Sometimes a programmer to do implementation-dependent, unsafe things, and using the reinterpret_cast operator makes it impossible to keep track of such acts. It has the same syntax as the other three operators:

```
reinterpret_cast <type-name> (expression)
```

Here is a sample use:

```
struct {long a; short b;};
long value = 0xA224B1B;
dat * pd = reinterpret_cast<dat *>(&value);
cout << hex << pd->da; // display first 2 bytes of value
```

Typically, type casts would be used for low-level, implementation-dependent programming and would not be portable. For example, one system may store the bytes in a multibyte value in a different order than does another system.

The reinterpret_cast operator doesn't allow just anything, however. For example, you can cast a pointer to an integer type that's large enough to hold the pointer representation, but you can't cast a pointer to a smaller integer or to a floating-point type. Another restriction is that you can't cast a function pointer to a data pointer or vice versa.

The plain type cast in C++ is also restricted. Basically, it can do anything the other type casts do, with some combinations, as a static_cast or reinterpret_cast followed by a const_cast, but it can't do anything else. Thus, the following type cast is allowed in C but, typically not in C++ implementations the char is too small to hold a pointer implementation:

```
char ch = char (&value); // type cast #2 - convert address to a char
```

These restrictions make sense, but if you found such enforced judgment oppressive, you still have C available.