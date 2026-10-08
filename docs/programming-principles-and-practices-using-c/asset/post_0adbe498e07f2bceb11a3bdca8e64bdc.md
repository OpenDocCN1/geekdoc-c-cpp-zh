
The representation of a **string** is a bit more complicated than that of an **int** because a **string** keeps track of the number of characters it holds. Note that a **double** stores a number whereas a **string** stores characters. For example, x stores the number 1.2, whereas s2 stores the three characters '1', ' ', and '2'. The quotes for character and string literals are not stored.

Every **int** is of the same size; that is, the compiler sets aside the same fixed amount of memory for each **int**. On a typical desktop computer, that amount is 4 bytes (32 bits). Similarly, **bools**, **chars**, and **doubles** are fixed size. You’ll typically find that a desktop computer uses a byte (8 bits) for a **bool** or a **char** and 8 bytes for a **double**. Note that different types of objects take up different amounts of space. In particular, a **char** takes up less space than an **int**, and **string** differs from **double**, **int**, and **char** in that different strings can take up different amounts of space.

The meaning of bits in memory is completely dependent on the type used to access it. Think of it this way: computer memory doesn’t know about our types; it’s just memory. The bits of memory get meaning only when we decide how that memory is to be interpreted. This is similar to what we do every day when we use numbers. What does 12.5 mean? We don’t know. It could be $12.5 or 12.5cm or 12.5gallons. Only when we supply the unit does the notation 12.5 mean anything.

For example, the very same bits of memory that represent the value 120 when looked upon as an **int** would be 'x' when looked upon as a **char**. If looked at as a **string**, it wouldn’t make sense at all and would become a run-time error if we tried to use it. We can illustrate this graphically like this, using 1 and 0 to indicate the value of bits in memory:

```
00000000 00000000 00000000 01111000
```

This is the setting of the bits of an area of memory (a word) that could be read as an **int** (120) or as a **char** ('x', looking at the rightmost 8 bits only). A **bit** is a unit of computer memory that can hold the value 0 or 1. For the meaning of *binary* numbers, see §A.2.1.1.

# 3.9 Type safety

Every object is given a type when it is defined. A program – or a part of a program – is type-safe when objects are used only according to the rules for their type. Unfortunately, there are ways of doing operations that are not type-safe. For example, using a variable before it has been initialized is not considered type-safe:

```
int main()
{
    double x;            // we "forgot" to initialize:
                        // the value of x is undefined
    double y = x;     // The value of y is undefined
    double z = 2.0+x;  // The meaning of + and the value of z are undefined
}
```

An implementation is even allowed to give a hardware error when the uninitialized **x** is used. Always initialize your variables! There are a few – very few – exceptions to this rule, such as a variable we immediately use as the target of an input operation, but always to initialize is a good habit that’ll save you a lot of grief.

Complete type safety is the ideal and therefore the general rule for the language. Unfortunately, a C++ compiler cannot guarantee complete type safety, but we can avoid type safety violations through a combination of good coding practice and run-time checks. The ideal is never to use language features that the compiler cannot prove to be safe: static type safety. Unfortunately, that’s too restrictive for most interesting uses of programming. The obvious fallback, that the compiler implicitly generates code that checks for type safety violations and catches all of them, is beyond C++. When we decide to do things that are (type) unsafe, we must do some checking ourselves. We’ll point out such cases as we get to them.

The ideal of type safety is incredibly important when writing code. That’s why we spend time on it this early in the book. Please note the pitfalls and avoid them.

## 3.9.1 Safe conversions

In §3.4, we saw that we couldn’t directly add **char** or compare a **double** to an **int**. However, C++ provides an indirect way to do both. When needed, a **char** is converted to an **int** and an **int** is converted to a **double**. For example:

```c
char c = 'x';
int i1 = c;
int i2 = 'x';
```

Here both **i1** and **i2** get the value **120**, which is the integer value of the character 'x' in the most popular 8-bit character set, ASCII. This is a simple and safe way of getting the numeric representation of a character. We call this **char**-to-**int** conversion safe because no information is lost; that is, we can copy the resulting **int** back into a **char** and get the original value:

```c
char c2 = i1;
cout << c << ' ' << i1 << ' ' << c2 << '\n';
```

This will print

```text
x 120 x
```

In this sense — that a value is always converted to an equal value or (for doubles) to the best approximation of an equal value — these conversions are safe:

- * bool to char
- bool to int
- bool to double
- char to int
- char to double
- int to double

The most useful conversion is int to double because it allows us to mix ints and doubles in expressions:

```cpp
double d1 = 2.3;
double d2 = d1+2;      // 2 is converted to 2.0 before adding
if (d1 < 0)             // 0 is converted to 0.0 before comparison
    cout << "d1 is negative";
```

For a really large int, we can (for some computers) suffer a loss of precision when converting to double. This is a rare problem.

## 3.9.2 Unsafe conversions

Safe conversions are usually a boon to the programmer and simplify writing code. Unfortunately, C++ also allows for (implicit) unsafe conversions. By unsafe, we mean that a value can be implicitly turned into a value of another type that does not equal the original value. For example:

```cpp
int main()
{
    int a = 20000;
    char c = a;           // try to squeeze a large int into a small char
    int b = c;
    if (a != b)           // != means "not equal"
        cout << "oops! " << a << "!=" << b << "\n";
    else
        cout << "Wow! We have large characters\n";
}
```

Such conversions are also called “narrowing” conversions, because they put a value into an object that may be too small (“narrow”) to hold it. Unfortunately, few compilers warn about the unsafe initialization of the **char** with an **int**. The problem is that an **int** is typically much larger than a **char**, so that it can (and in this case does) hold an **int** value that cannot be represented as a **char**. Try it to see what value *b* gets on your machine (32 is a common result); better still, experiment:

```cpp
int main()
{
    double d = 0;
    while (cin>>d) {
        // repeat the statements below
        // as long as we type in numbers
        int i = d;      // try to squeeze a double into an int
        char c = i;     // try to squeeze an int into a char
        int i2 = c;     // get the integer value of the character
        cout << "d==" << d              // the original double
             << " i=="<< i              // converted to int
             << " i2==" << i2           // int value of char
             << " char(" << c << ")"<<"\n";  // the char
    }
}
```

The **while**-statement that we use to allow many values to be tried will be explained in §4.4.2.1.

# TRY THIS

Run this program with a variety of inputs. Try small values (e.g., **2** and **3**); try large values (larger than **127**, larger than **1000**); try negative values; try **56**; try **89**; try **128**; try non-integer values (e.g., **56.9** and **56.2**). In addition to showing how conversions from **double** to **int** and conversions from **int** to **char** are done on your machine, this program shows you what character (if any) your machine will print for a given integer value.

You'll find that many input values produce “unreasonable” results. Basically, we are trying to put a gallon into a pint pot (about 4 liters into a 500ml glass). All of the conversions

- **double** to **int**
- **double** to **char**
- **double** to **bool**
- **int** to **char**
