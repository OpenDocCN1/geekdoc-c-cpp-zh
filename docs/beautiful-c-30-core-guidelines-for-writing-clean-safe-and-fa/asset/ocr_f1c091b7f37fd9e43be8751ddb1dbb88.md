Even name mangling isn’t immune from ABI breaks. An ABI can define a stand-ard way of uniquely identifying the name of a function so that libraries built with different languages, for example C and Pascal, can be linked together. If you have ever seen the declaration `extern "C"` in a header file, that is a signal to the compiler that the function names within the declaration should have their names inserted into the exports table using the same naming scheme as a C compiler on that platform would use.

The earlier hypothetical problem with a library that takes a `std::string` is unlikely to trouble you. Today’s linkers will simply prevent clients of different stand-ard libraries from linking. There are a number of ways to do this: the ABI version can be embedded in the mangled name of the symbol, or the compiler can insert the ABI version into the object file and emit an error should anyone try to link conflicting ver-sions together. The labor of dealing with conflicting ABIs is not eliminated, but it is exposed and added to the engineer’s plate.

Recall the guideline: “If you want a cross-compiler ABI, use a C-style subset.” We have now explained the nature of a cross-compiler ABI, and why observing it is important for both today and the future. Let us now move on to the C-style subset.

# Paring back to the absolute minimum

So, what does a C-style subset consist of? The C types are often referred to as the built-in types. They are the types that are not made up of any other types. I would say they are the atomic types, but sadly that has another meaning in C++. You can, however, think of them as the fundamental building blocks of all your types. The list consists of²

2. https://en.cppreference.com/w/cpp/language/types

```
void
bool
char
int
```