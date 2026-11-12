
## Concurrent Safe bit-fields

Two bit-fields are safe for concurrent updates by two threads, if they are located in separate memory locations

- *bitfield_b* and *bitfield_c* are located in the same memory location, hence not thread-safe for concurrent updates.
- *bitfield_c* and *bitfield_d* are located in different memory locations because they are separated by a zero-length bit-field, hence thread-safe for concurrent updates.
- *bitfield_d* and *bitfield_a1* are located in different memory locations because *bitfield_a1* is inside the nested structure E, hence thread-safe for concurrent updates.
- *bitfield_f* and *bitfield_h* are located in different memory locations because these are separated by a *non-bitfield* data member *non_bitfield_g*, hence thread-safe for concurrent updates.

Hence it is not safe to concurrently update two bit-fields in the same struct if all fields between them are also bit-fields of non-zero width because these constitute the same memory location.

There are seven memory locations associated with the structure A

- 1. *non_bitfield_a*
- 2. *bitfield_b* and *bitfield_c*
- 3. *bitfield_d*
- 4. *bitfield_a1* (*non_bitfield_e*)
- 5. *bitfield_f*
- 6. non_bitfield_g
- 7. bitfield_h

```c
struct A
{
    char non_bitfield_a;
    int bitfield_b    : 3;
    int bitfield_c    : 10;
    int               : 0;

    int bitfield_d    : 8;

    struct E
    {
        int bitfield_a1 : 8;
    } non_bitfield_e;

    int bitfield_f    : 4;
    int non_bitfield_g;
    int bitfield_h    : 11;
};
```

## Question 2 Distinct Address Location

What happens when the program below is compiled ?

Program 8.3: Distinct Address Location

```cpp
int main()
{
    char a = 'a';
    char b = 'b';
    static_assert(&a == &b, "Address_of_a_and_b_"
                          "should_be_distinct");
}
```

### Solution of Question 2

It results into a compilation error as enlisted below:

```text
distinct_add.cpp: In function 'int main()':
distinct_add.cpp:6:6:
error: static assertion failed:
Address of a and b should be distinct
     static_assert(&a == &b, "Address of a and b "
     ^
```

Address location of two distinct objects is always distinct except when the following is true in which case the result is implementation-defined:

- 1. These are bit-fields
- 2. These are base-class sub-objects of zero size

The address of an object is the address of the first byte it occupies except when it is either a bit-field or a base class sub-object of zero size.

## Question 3 Signal and Values

List the types of the objects whose values are guaranteed to be defined even in case of signals ?

### Solution of Question 3

- 1. volatile std::sig_atomic_t
- 2. lock-free atomic objects

## Question 4 Temporary and Conversions

In the program below, what happens before temporary gets destroyed in line 12

Program 8.4: Temporary and Conversions

```cpp
struct A
{
    A(int x) : _x(x) {}

    int & val() { return _x; }
private:
    int _x;
};

int main()
{
    if(A(1).val())
    {}
}
```

### Solution of Question 4

The following conversion takes place before destruction of the temporary object of type A

- 1. lvalue to rvalue conversion
- 2. int to bool conversion

## Question 5 evaluation of expressions

Review the program below:

Program 8.5: evaluation of expressions

```cpp
void compute(int, int) {}
void eval(int x, int arr[])
{
    x = arr[x++];

    x = 2, x++, x++;

    x = x++ + 1;
    x = x + 1;

    compute(x = -1, x = -1);
}
```

### Solution of Question 5

- line 5: behavior is undefined
- line 7: x becomes 4
- line 9: behavior is undefined
- line 10: the value of x is incremented
- line 12: behavior is undefined

## Question 6 trigraph sequences

What happens with the trigraphs here:

```
Program 8.6: trigraph sequences
1??=define validateArray(x, y) x??(y??) ??!??! y??(x??)
```

### Solution of Question 6

- trigraph ??= is replaced by #
- trigraph ??( is replaced by [
- trigraph ??) is replaced by ]
- trigraph ??! is replaced by |

The above ⇒ that the stated trigraph sequences will be replaced to change the expression to look like below

```
Program 8.7: replacing trigraph sequences
1#define validateArray(x, y) x[y] || y[x]
```

## Question 7 increment operator

What is the output of the program:

```
Program 8.8: increment operator
1#include <iostream>
2
3int main()
4{
5    int one = 1;
6    int two = 2;
7
8    int a = one+++++two;
9 }
```

### Solution of Question 7

When compiled, the error is:

```text
increment_operator.cpp: In function ‘int main()’:
increment_operator.cpp:8:18:
error: lvalue required as increment operand
    int a = one+++++two;
```

The expression `one+++++two` is parsed to look like `one ++ ++ + two`, which violates a constraint on increment operators, thus leading to incorrect expression.

*one+++++two ⇒ one ++ ++ + two*

Please note that the expression `one+++++two` is not parsed as `one ++ + ++ two`, which is indeed a correct expression.

*one+++++two ⇒ one ++ ++ + two*

## Question 8 — nullptr

What is `nullptr`?

### Solution of Question 8

`nullptr` is the pointer literal designating a prvalue of type `std::nullptr_t`. It is a null pointer constant which can be converted to a null pointer value or a null member pointer value.

Please note that `std::nullptr_t` itself

- is not a pointer type
- is not a pointer to member type
- is a distinct type

## Question 9 — user defined literal

What is *user defined literal*?

### Solution of Question 9

A *user defined literal* is a call to a literal operator or literal operator template of the form

- 1. `operator "" identifier`
- 2. `operator "" identifier<'c₁', 'c₂', ..., 'cₖ'>()`

For example:

- 1. `user-defined-integer-literal`
  - a) `operator "" identifier (n ULL)`
  - b) `operator "" identifier ("n")`
  - c) `operator "" identifier <'c1', 'c2', ... 'ck'>()`
- 2. *user-defined-floating-literal*
  - a) `operator "" identifier (f L)`
  - b) `operator "" identifier ("ff")`
  - c) `operator "" identifier <'c1', 'c2', ... 'ck'>()`
- 3. *user-defined-string-literal*
  - a) `operator "" identifier (str, len)`
  - b) `operator "" identifier (ch)`
  - c) `operator "" identifier <'c1', 'c2', ... 'ck'>()`

Program 8.9: user defined literal

```cpp
#include <string>

void operator "" _distance(long double);
long double operator "" _amount(long double);

std::string operator "" _amount(const char16_t *,
                                std::size_t);

unsigned operator "" _amount(const char*);
float operator "" _X(const char*);

template <char...> int operator "" _length();

int main()
{
    2.9_amount;

    u"test"_amount;

    20_amount;
}
```

In the example above

- line 18 calls operator "" _amount(2.9L)
- line 20 calls operator "" _amount(u"test", 4)
- line 22 calls operator "" _amount("20")

## Question 10 Declaration vs Definition

Which of the following are definitions and which are just declarations?

Program 8.10: Declaration vs Definition

```cpp
1 extern int a1;
2 int a2;
3 extern const int a3;
4 extern const int a4 = 10;
5 void fun(int);
6 void fun(int) {}
7 struct A;
8 struct A
9 {
10     int x, y;
11 };
12 typedef int Integer;
13 enum { low, mid, high };
14 extern A _A;
15 struct B
16 {
17     static int x;
18 };
19 int B::x = 5;
20 namespace Detail { int x; }
21 using Detail::x;
22 namespace DetailsX = Detail;
23 B b1;
```

### Solution of Question 10

- *Declarations*  
  line 1, 3, 5, 7, 12, 14, 17, 21
- *Definitions*  
  Rest are definitions

## Question 11 — Compiler Generated Member Functions

In the following case, list the member functions whose definitions are implicitly generated by the compiler:

Program 8.11: Sample Class

```cpp
1 #include <string>
2 struct A
3 {
4     std::string __str;
5 };
6 
7 int main()
8 {
9     A a1;
10    A a2 = a1;
11    a2 = a1;
12 }
```
