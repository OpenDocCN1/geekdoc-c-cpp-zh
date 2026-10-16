Unions, however, are not needed in object-oriented languages, since a better design is to use inheritance to represent different nonoverlapping data requirements (see Chapter 5). Thus, Java does not have unions. C++ does retain unions, presumably primarily for compatibility with C.

Even in C, however, unions cause a small but significant problem. Typically, unions are used as a variant part of a struct. This requires that an extra level of member selection must be used, as in the `struct IntOrReal` definition above, where we had to use `x.val.i` and `x.val.r` to address the overlapping data. C++ offers a new option here—the **anonymous union** within a `struct` declaration, and we could write `struct IntOrReal` in C++ as follows:

```
```cpp
enum Disc {IsInt,IsReal};
struct IntOrReal { // C++ only!
    enum Disc which;
    union{
        int i;
        double r;
    }; // no member name here
};
```
```

Now we can address the data simply as `x.i` and `x.r`. Of course, Ada already has this built into the syntax of the variant record.

# 8.3.3 Subset

In mathematics, a subset can be specified by giving a rule to distinguish its elements, such as `pos_int = {x | x is an integer and x > 0}`. Similar rules can be given in programming languages to establish new types that are subsets of known types. Ada, for example, has a very general **subtype** mechanism. By specifying a lower and upper bound, subranges of ordinal types can be declared in Ada, as for example:

```
```ada
subtype IntDigit_Type is integer range 0..9;
```
```

Compare this with the simple type defined in Section 8.2:

```
```ada
type Digit_Type is range 0..9;
```
```

which is a completely new type, **not** a subtype of **integer**.

Variant parts of records can also be fixed using a subtype. For example, consider the Ada declaration of `IntOrReal` in the preceding section a subset type can be declared that fixes the variant part (which then must have the specified value):

```
```ada
subtype IRInt is IntOrReal(IsInt);
subtype IRReal is IntOrReal(IsReal);
```
```

Such subset types **inherit** operations from their parent types. Most languages, however, do not allow the programmer to specify which operations are inherited and which are not. Instead, operations are automatically or implicitly inherited. In Ada, for example, subtypes inherit all the operations of the parent type. It would be nice to be able to exclude operations that do not make sense for a subset type; for example, unary minus makes little sense for a value of type **IntDigit_Type**.