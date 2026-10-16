
```
‘a’ // char
1ULL // unsigned long long
0xD0 // hexadecimal unsigned
"as" // C-style string (const char[3])
```

In addition, we can define literals for user-defined types and new forms of literals for built-in types. For example:

```
“Hi!”s // string, not “zero-terminated array of char”
1.2i // imaginary
101010111000101b // binary
123s // seconds
123.56km // not miles! (units)
1234567890123456789012345678901234567890x // extended-precision
```

Such user-defined literals are supported through the notion of literal operators that map literals with a given suffix into a desired type. The name of a literal operator is operator""" followed by the suffix. For example:

```
constexpr complex<double> operator"""i(long double d) // imaginary literal
{
return {0,d}; // complex is a literal type
}
```

```
std::string operator"""s(const char* p, size_t n) // std::string literal
{
return string{p,n}; // requires free-store allocation
}
```

These two operators define suffixes i and s, respectively. I use constexpr to enable compile-time evaluation. Given those, we can write:

```
template<typename T> void f(const T&);

void g() {
f("Hello"); // pass pointer to char*
f("Hello"s); // pass (five-character) string object f("Hello\n"s); // pass (six-character) string object

auto z = 2+1i; // complex{2,1}
}
```

The basic (implementation) idea is that after parsing what could be a literal, the compiler always checks for a suffix. The user-defined literal mechanism simply allows the user to specify a new suffix and define what is to be done with the literal before it. It is not possible to redefine the meaning of a built-in literal suffix or to augment the syntax of literals.

There are four kinds of literals that can be suffixed to make a user-defined literal (§iso.2.14.8):

- An integer literal (§6.2.4.1): accepted by a literal operator taking an unsigned long long or a **const char*** argument or by a template literal operator, for example, **123m** or **12345678901234567890X**
- A floating-point literal (§6.2.5.1): accepted by a literal operator taking a **long double** or a **const char*** argument or by a template literal operator, for example, **12345678901234567890.976543210x** or **3.99s**
- A string literal (§7.3.2): accepted by a literal operator taking a (**const char***, **size_t**) pair of arguments, for example, **“string”s** and **R”(Foo\bar)”_path**
- A character literal (§6.2.3.2): accepted by a literal operator taking a character argument of type **char**, **wchar_t**, **char16_t**, or **char32_t**, for example, **‘f’_runic** or **u’ BEEF’_w**. For example, we could define a literal operator to collect digits for integer values that cannot be represented in any of the built-in integer types:

```
Bignum operator""" x(const char* p)
{
return Bignum(p);
}
```

```
void f(Bignum);
f(123456789012345678901234567890123456789012345x);
```

Here, the C-style string “123456789012345678901234567890123456789012345” is passed to operator""" x(). Note that I did not put those digits in double quotes. I requested a C-style string for my operator, and the compiler delivered it from the digits provided.

To get a C-style string from the program source text into a literal operator, we request both the string and its number of characters. For example:

```
string operator""" s(const char* p, size_t n);
```

```
string s12 = “one two”s; // calls operator ""("one two",7)
string s22 = “two\ntwo”s; // calls operator ""("two\ntwo",7)
string sxx = R”(two\ntwo)”s; // calls operator ""("two\ntwo",8)
```

In the raw string (§7.3.2.1), “\n” represents the two characters ‘\’ and ‘n’.

The rationale for requiring the number of characters is that if we want to have “a different kind of string,” we almost always want to know the number of characters anyway.

A literal operator that takes just a **const char*** argument (and no size) can be applied to integer and floating-point literals. For example:

```
string operator""" SS(const char*p); // warning: this will not work as expected
string s12 = “one two”SS; string s13 = 13SS;
// error :no applicable literal operator // OK, but why would anyone do that? A literal operator converting numerical values to strings could be quite confusing. A template literal operator is a literal operator that takes its argument as a template parameter pack, rather than as a function argument. For example:
```

```
template<char...>
constexpr int operator""" _b3(); // base 3, i.e., ternary
```

The relatively simple string class presented in this section illustrates several techniques that are useful for the design and implementation of classes using conventionally defined operators. This String is a simplified version of the standard-library string (§4.2, Chapter 36). String provides value semantics, checked and unchecked access to characters, stream I/O, support for rangefor loops, equality operations, and concatenation operators. I also added a String literal, which std::string does not (yet) have.

To allow simple interoperability with C-style strings (including string literals (§7.3.2)), I represent strings as zero-terminated arrays of characters. For realism, I implement the short string optimization. That is, a String with only a few characters stores those characters in the class object itself, rather than on the free store. This optimizes string usage for small strings. Experience shows that for a huge number of applications most strings are short. This optimization is particularly important in multi-threaded systems where sharing through pointers (or references) is infeasible and free-store allocation and deallocation relatively expensive.

To allow Strings to efficiently “grow” by adding characters at the end, I implement a scheme for keeping extra space for such growth similar to the one used for vector (§13.6.1). This makes String a suitable target for various forms of input.

Writing a better string class and/or one that provides more facilities is a good exercise. That done, we can throw away our exercises and use std::string (Chapter 36).

## 19.3.1 Essential Operations

Class String provides the usual set of constructors, a destructor, and assignment operations (§17.1):

```
class String {
public:
String(); // default constructor :x{""}
explicit String(const char*p); // constructor from C-style string: x{"Euler"}
String(const String&); // copyconstructor String& operator=(const String&); // copyassignment String(String&& x); // moveconstructor String& operator=(String&& x); // moveassignment
~String() { if (short_max<sz) delete[] ptr; } // destructor
// ...
};
```

This String has value semantics. That is, after an assignment s1=s2, the two strings s1 and s2 are fully distinct, and subsequent changes to one have no effect on the other. The alternative would be to give String pointer semantics. That would be to let changes to s2 after s1=s2 also affect the value of s1. Where it makes sense, I prefer value semantics; examples are complex, vector, Matrix, and string. However, for value semantics to be affordable, we need to pass Strings by reference when we don’t need copies and to implement move semantics (§3.3.2, §17.5.2) to optimize return.

The slightly nontrivial representation of String is presented in §19.3.3. Note that it

requires user-defined versions of the copy and move operations.

## 19.3.2 Access to Characters

The design of access operators for a string is a difficult topic because ideally access is by conventional notation (that is, using []), maximally efficient, and range checked.
Unfortunately, you cannot have all of these properties simultaneously. Here, I follow the standard library by providing efficient unchecked operations with the conventional [] subscript notation plus range-checked at() operations:

```
class String { public:
//...
char& operator[](int n) { return ptr[n]; } char operator[](int n) const { return ptr[n]; }
// unchecked element access
char& at(int n) { check(n); return ptr[n]; } char at(int n) const { check(n); return ptr[n]; }
// range-checked element access
String& operator+=(char c); // add c at end
const char* c_str() { return ptr; } const char* c_str() const { return ptr; }
// C-style string access
int size() const { return sz; } int capacity() const
// number of elements
// elements plus available space { return (sz<=short_max) ? short_max : sz+space; }
//...
};
```

The idea is to use [] for ordinary use. For example:

Section 19.3.2 Access to Characters 563

```
int hash(const String& s) {
int h {s[0]};
for (int i {1}; i!=s.size(); i++) h ^= s[i]>>1; return h;
}
// unchecked access to s
```

Here, using the checked at() would be redundant because we correctly access s only from 0 to s.size()-1.

We can use at() where we see a possibility of mistakes. For example:

```
void print_in_order(const String& s,const vector<int>& index)
{
for (x : index) cout << s.at(x) << '\n';
}
```

Unfortunately, assuming that people will use at() consistently where mistakes can be made is overly optimistic, so some implementations of std::string (from which the []/at() convention is borrowed) also check []. I personally prefer a checked [] at least during
