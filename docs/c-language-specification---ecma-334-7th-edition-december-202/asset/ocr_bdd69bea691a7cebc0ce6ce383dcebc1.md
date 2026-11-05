```
: 'new'
| 'public'
| 'internal'
| 'private'
| 'unsafe'
;
```

```
buffer_element_type
: type
;
```

```
fixed_size_buffer_declarators
: fixed_size_buffer_declarator (',' fixed_size_buffer_declarator)*
;
```

```
fixed_size_buffer_declarator
: identifier '[' constant_expression ']'
;
```

A fixed-size buffer declaration may include a set of attributes (§22), a new modifier (§15.3.5), accessibility modifiers corresponding to any of the declared accessibilities permitted for struct members (§16.4.3) and an unsafe modifier (§23.2). The attributes and modifiers apply to all of the members declared by the fixed-size buffer declaration. It is an error for the same modifier to appear multiple times in a fixed-size buffer declaration.

A fixed-size buffer declaration is not permitted to include the static modifier.

The buffer element type of a fixed-size buffer declaration specifies the element type of the buffer(s) introduced by the declaration. The buffer element type shall be one of the predefined types sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, or bool.

The buffer element type is followed by a list of fixed-size buffer declarators, each of which introduces a new member. A fixed-size buffer declarator consists of an identifier that names the member, followed by a constant expression enclosed in [ and ] tokens. The constant expression denotes the number of elements in the member introduced by that fixed-size buffer declarator. The type of the constant expression shall be implicitly convertible to type int, and the value shall be a non-zero positive integer.

The elements of a fixed-size buffer shall be laid out sequentially in memory.

A fixed-size buffer declaration that declares multiple fixed-size buffers is equivalent to multiple declarations of a single fixed-size buffer declaration with the same attributes, and element types.

*Example:*

```
unsafe struct A
{
    public fixed int x[5], y[10], z[100];
}
```

is equivalent to

```
unsafe struct A
{
    public fixed int x[5];
    public fixed int y[10];
    public fixed int z[100];
}
```