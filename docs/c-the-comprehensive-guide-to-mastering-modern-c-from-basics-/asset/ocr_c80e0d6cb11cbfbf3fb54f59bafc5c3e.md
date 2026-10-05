This loop reads in exactly 100 lines. As soon as idx reaches zero, the loop is terminated. The int value of idx is implicitly converted into a bool. This is done according to the following rules, which take some getting used to:

+   - A value of of is converted to false.
- All other values become true.

Because C++ programmers originally came from C, where there was no pure bool data type, you will encounter this pattern quite often.

You can also use other data types in tests. To do this, the data type only needs to have the operator bool() method. This is the case, for example, with std::string and therefore with std::cin. You can see in application example in the while loop in Chapter 27, Listing 27.6.

# 4.4.6 Character Types

What is a “character” in abstract terms? It is a building block of text that is to be displayed or processed. In C++, many things are mixed up here, and some things are not intuitive.

The main data type for characters is char. At the same time, however, you can also regard char as an integer data type, as you can calculate with it in the same way as with other int relatives. And yet it is different, because it is not specified whether char is signed or unsigned without further specifications. So if you want to calculate with a char and the range is important, then you should always write signed or unsigned instead of simply char; reserve the latter for texts.

> “char” is the Smallest “int”

It is even specified that char is the smallest integer data type and something like a base unit for memory usage. If you apply sizeof(...) to any type or value, you get its size in char units:

```
sizeof(char); // 1
char x;
sizeof(x); // 1
int value;
sizeof(value); // 4 or something else on other systems
```

On current systems, you can assume that a char has eight bits. Because you cannot rely on the sign, you should only assume that the