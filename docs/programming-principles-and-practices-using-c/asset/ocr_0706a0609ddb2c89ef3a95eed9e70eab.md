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
```