| Category | Operators | Restrictions |
|----------|-----------|--------------|
| Arithmetic binary | + , * , / , - , % | None |
| Arithmetic unary | + , - , ++ , -- | None |
| Bitwise binary | & , | , ^ , << , >> | None |
| Bitwise unary | ! , ~ , true , false | The true and false operators must be overloaded as a pair. |
| Comparison | == , != , > , >= , <= , < , <=> | Comparison operators must be overloaded in pairs. |
| Assignment | += , -= , *= , /= , >>= , <<= , %= , &= , |= , ^= | You cannot explicitly overload these operators; they are overridden implicitly when you override the individual operators such as + , - , % , and so on. |
| Index | [] | You cannot overload the index operator directly. The indexer member type, discussed in Chapter 2, allows you to support the index operator on your classes and structs. |
| Cast | () | You cannot overload the cast operator directly. User-defined casts (discussed in the last section of this chapter) allow you to define custom cast behavior. |

> > NOTE You might wonder what is the reason for overloading the true and false operators. There’s a good reason: what integer value is true or false is different based on the technology or framework you use. With many technologies, 0 is false and 1 is true; others define that any other value than 0 is true. You can also find technologies where –1 is false.

# # Implementing Custom Index Operators

Custom indexers cannot be implemented using the operator overloading syntax, but they can be implemented with a syntax that looks very similar to properties.

Start by looking at accessing array elements. Here, an array of int elements is created. The second code line uses the indexer to access the second element and pass 42 to it. The third line uses the indexer to access the third element and pass the element to the variable x.

```
```
int[] arr1 = {1, 2, 3};
arr1[1] = 42;
int x = arr1[2];
```
```