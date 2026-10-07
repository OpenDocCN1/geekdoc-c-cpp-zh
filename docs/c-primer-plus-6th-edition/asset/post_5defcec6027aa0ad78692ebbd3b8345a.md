
# Simple Variables

These distinctions are particularly important if you use char as a numeric type. The unsigned char type typically represents the range 0 to 255, and signed char typically represents the range -128 to 127. For example, suppose you want to use a char variable to hold values as 200. That works on some systems but fails on others. You can, however, successfully use unsigned char for that purpose on any system. On the other hand, if you use a char variable to hold a standard ASCII character, it doesn't matter whether char is signed or unsigned, so you can use char.

# For When You Need More: wchar_t

Programs might have to handle characters that don't fit within the confines of a single 8-bit byte (the Japanese kanji system). C++ handles this in a couple ways. First, if a large set of characters is the basic character for an implementation, a compiler can define char as a 16-byte or larger. Second, an implementation can support both a small basic set and a larger extended set. The usual 8-bit char can represent the basic character, and another type, called wchar_t (for wide character type), the wchar_t type is an integer type with sufficient space to represent the extended set used on the system. It has the same size and properties as one of the other integer types, which is called the underlying type. The choice of type depends on the implementation, so it could be unsigned short on one system and int on another.

```cpp
wchar_t bob = L'LP'; // a wide-character constant
wcout << L"total" << endl; // outputting a wide-character string
```

On a system with 2-byte wchar_t, this code stores each character in a 2-byte unit of memory. This book doesn't use the wchar-character type, but you should be aware of, particularly if you become involved in international programming or in using Unicode or ISO 10646.

# New C++11 Types: char16_t and char32_t

As the programming community gained more experience with Unicode, it became clear that the wchar_t wasn't enough. It turns out that encoding characters and strings of characters on a computer system is more complex than just using the Unicode values (called code points). In particular, it is useful, when encoding characters, to have a type of definite size and signedness. The bit and size of wchar_t can vary from one implementation to another. So C++11 introduces the types char16_t, which is unsigned and 16 bits, and char32_t, which is unsigned and 32 bits. C++11 uses the u prefix for char16_t character and string constants, as in 'uC' and u"be good". Similarly, it uses the U prefix for char32_t constants, as in U'R' and U"dirty rat". The char16_t is a natural match for universal character names of the form \u00F6, and the char32_t is a natural match for universal character names of the form \U0000222B. The prefixes u and U are used to indicate character literals of types char16_t and char32_t, respectively:

```cpp
char16_t chl = u'q'; // basic character in 16-bit form
char32_t ch22 = U'\U0000222B'; // universal character name in 32-bit form
```

Like wchar_t, char16_t and char32_t each have an underlying type, which is one of the built-in types. But the underlying type can be different on one system with what it is on another.

# The bool Type

The ANSI/ISO C++ has added a new type (new to C++, that is), called bool. Named in honor of the English mathematician George Boole, who developed a mathematical representation of the laws of logic. In computing, a Boolean variable is one whose value can be either true or false. In the C++, like C, has not had a Boolean type. Instead, as you'll see greater detail in Chapters 5 and 6, C++ interprets nonzero as true and zero false as values. Now, you can use the bool type to represent true and false, and the predefined true and false represent those values. That is, you make statements like the following:

```cpp
bool is_ready = true;
```

The literals true and false can be converted to int by promotion, which true converting to 1 and false to 0:

```cpp
int ans = true; // ans assigned 1
int promise = false; // promise assigned 0
```

Any numeric or pointer value can be converted implicitly (that is, without an explicit type cast). Any nonzero value converts to true, whereas a zero value converts to false:

```cpp
bool start = -100; // start assigned true
bool stop = 0; // stop assigned false
```

After the book introduces statements (in Chapter 6, "Branching Statements and Logical Operators"), the bool type will become a common feature in the examples.

# The const Qualifier

Now letss return to the topic of symbolic names for constants. Symbolic name can suggest what the constant represents. If the program uses the constant in several places you need to change the value, you can just change the single symbol definition. The note #define statements earlier in this chapter (see the sidebar "Symbolic Constants Preprocessor Way") shows that C++ has a better way to handle constants. The way is to use the const qualifier. This tells the compiler that the variable cannot be modified after its initialization. If the program uses the constant in several places you need to change the value, you can just change the single symbol definition. The way is to use the const qualifier. This tells the compiler that the variable cannot be modified after its initialization. If the program uses the constant in several places you need to change the value, you can just change the single symbol definition. The way is to use the const qualifier. This tells the compiler that the variable cannot be modified after its initialization. Suppose, for example,

```cpp
const int Months = 12;
```

If you try to change the value, the compiler will generate an error. This ensures that the constant is never accidentally changed during the execution of the program.
