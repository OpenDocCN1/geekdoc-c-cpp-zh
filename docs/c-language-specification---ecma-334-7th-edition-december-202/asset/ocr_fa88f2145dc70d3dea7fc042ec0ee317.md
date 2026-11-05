```
public class C
{
    private int _value;
    public C(int value) => _value = value;
    public ref int GetPinnableReference() => ref _value;
}

public class Test
{
    unsafe private static void Main()
    {
        C c = new C(10);
        fixed (int* p = c)
        {
            // ...
        }
    }
}
```

Type C has an accessible GetPinnableReference method with the correct signature. In the fixed statement, the ref int returned from that method when it is called on c is used to initialize the int* pointer p. end example

Modifying objects of managed type through fixed pointers can result in undefined behavior.

Note: For example, because strings are immutable, it is the programmer’s responsibility to ensure that the characters referenced by a pointer to a fixed string are not modified. end note

Note: The automatic null-termination of strings is particularly convenient when calling external APIs that expect “C-style” strings. Note, however, that a string instance is permitted to contain null characters. If such null characters are present, the string will appear truncated when treated as a null-terminated char*. end note

# 23.8 Fixed-size buffers

# 23.8.1 General

Fixed-size buffers are used to declare “C-style” in-line arrays as members of structs, and are primarily useful for interfacing with unmanaged APIs.

# 23.8.2 Fixed-size buffer declarations

A fixed-size buffer is a member that represents storage for a fixed-length buffer of variables of a given type. A fixed-size buffer declaration introduces one or more fixed-size buffers of a given element type.

Note: Like an array, a fixed-size buffer can be thought of as containing elements. As such, the term element type as defined for an array is also used with a fixed-size buffer. end note

Fixed-size buffers are only permitted in struct declarations and may only occur in unsafe contexts (§23.2).

```
fixed_size_buffer_declaration
: attributes? fixed_size_buffer_modifier* 'fixed' buffer_element_type
  fixed_size_buffer_declarators ';'

fixed_size_buffer_modifier
```