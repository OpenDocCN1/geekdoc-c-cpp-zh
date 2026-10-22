example, in [Click here to view code image](#)

```
List<List<int>> a;
// ^-- no space between right angle brackets
```

the two > characters combine into a right-shift token >> and hence are never treated as two separate tokens *by the tokenizer*. This is a consequence of the *maximum munch* tokenization principle: A C++ implementation must collect as many consecutive characters as possible into a token.

As mentioned in Section 2.2 on page 28, since C++11, the C++ standard specifically calls out this case—where a nested template-id is closed by a right-shift token >>—and, within the parser, treats the right shift as being equivalent to two separate right angle brackets > and > to close two template-ids at once. It’s interesting to note that this change silently changes the meaning of some—admittedly contrived—programs. Consider the following example: [Click here to view code image](#)

```
names/anglebrackethack.cpp

#include <iostream>

template<int I> struct X {
static int const c = 2;
};

template<> struct X<0> {
typedef int c;
};

template<typename T> struct Y {
static int const c = 3;
};

static int const c = 4;

int main()
{
std::cout << (Y<X<1> >::c >::c) << ' ';
std::cout << (Y<X< 1> >::c >::c) << '\n';
}
```

This is a valid C++98 program that outputs **0 3**. It is also a valid C++11 program, but there the angle bracket hack makes the two parenthesized expressions equivalent, and the output is **0 0**.

A similar problem existed because of the existence of the digraph <: as an alternative for the source character [ (which is not available on some traditional