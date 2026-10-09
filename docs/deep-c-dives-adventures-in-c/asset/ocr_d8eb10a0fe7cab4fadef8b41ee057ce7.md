These suffixes were essential before C99, but after this constants take their type from what they are assigned to and they can generally be ignored. The C99 rule is that the type of a constant is the first type that is large enough to represent it from the list int, long, long  long.

You can also use hex and octal constants. Hex constants start with 0X and octal constants start with 0 and hence are error prone if you accidentally add a leading 0 to a decimal value. C23 has also added, at long last, binary constants which start 0b.

If you create a constant that has more bits than required then the remaining bits are simply ignored. For example:

```
char a = 0x010203040;
```

stores 0x40 in a. You will probably see a warning from the compiler and perhaps from a linter, but it works.

If the constant has a sign then it is assumed to be a signed value and it is converted to two's-complement form. This can be assigned to an unsigned variable and the bit pattern will be unchanged, but its value will be interpreted as positive. For example:

```
unsigned int a = -1;
```

assigns 0xFFFFFFFF to a as this is the two's-complement representation of -1. One literal that might confuse you is a character literal, for example:

```
unsigned int a = 'C'
```

is an int bit pattern corresponding to the ASCII code for the character – see later.

# Precise Types

Not being able to exactly specify the number of bits a variable can store is mostly a minor irritation, but there are arguments that making the size and signedness of a variable explicit is a good idea. For this reason many programmers define their own precise bit-size types and in C99 this was standardized.

You can use the type int_n_t  and uint_n_t  for a signed and unsigned integer with $n$ bits respectively. The value of $n$ is usually one of 8, 16, 32 and 64, but notice that if a system doesn't support a bit size then it simply omits the definition and your program will not compile.

Notice that the int_n_t and uint_n_t types are nearly always mapped to the older type specifiers on a given system, for example:

```
typedef signed char int8_t;
```