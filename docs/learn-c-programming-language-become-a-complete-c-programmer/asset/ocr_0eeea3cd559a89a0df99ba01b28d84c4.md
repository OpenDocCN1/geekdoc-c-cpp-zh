```
void f(int i) {
bool b {i!=0};
// ...
};
```

In arithmetic and logical expressions, **bool** are converted to **int**; integer arithmetic and logical operations are performed on the converted values. If the result needs to be converted back to **bool**, a **0** is converted to **false** and a nonzero value is converted to **true**. For example:

```
bool a = true; bool b = true;
```

```
bool x = a+b; bool y = a||b; bool z = a-b;
```

```
// a+b is 2, so x becomes true
// a||b is 1, so y becomes true ("||" means "or") // a-b is 0, so z becomes false
```

A pointer can be implicitly converted to a **bool** (§10.5.2.5). A non-null pointer converts to **true**; pointers with the value **nullptr** convert to **false**. For example:

```
void g(int * p)
{
bool b = p; // narrows to true or false bool b2 {p!=nullptr}; // explicit test against nullptr
if (p) { // equivalent to p!=nullptr
// ...
}
}
```

I prefer **if (p)** over **if (p!=nullptr)** because it more directly expresses the notion “if **p** is valid” and also because it is shorter. The shorter form leaves fewer opportunities for mistakes.

# 6.2.3 Character Types

There are many character sets and character set encodings in use. C++ provides a variety of character types that reflect that – often bewildering – variety:

+   - **char**: The default character type, used for program text. A **char** is used for the implementation’s character set and is usually 8 bits.
+   - **signed char**: Like **char**, but guaranteed to be signed, that is, capable of holding both positive and negative values.
+   - **unsigned char**: Like **char**, but guaranteed to be unsigned.
+   - **wchar_t**: Provided to hold characters of a larger character set such as Unicode (see §7.3.2.2). The size of **wchar_t** is implementation-defined and large enough to hold the largest character set supported by the implementation’s locale (Chapter 39).
+   - **char16_t**: A type for holding 16-bit character sets, such as UTF-16.
+   - **char32_t**: A type for holding 32-bit character sets, such as UTF-32.

These are six distinct types (despite the fact that the _t suffix is often used to denote aliases; §6.5). On each implementation, the **char** type will be identical to that of either **signed char** or **unsigned**