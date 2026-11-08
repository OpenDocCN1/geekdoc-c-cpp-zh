We’re sure you realize that this arbitrary interchange between using a pointer and using the original variable is not the right way to do this calculation. However, the example does demonstrate that using a dereferenced pointer is the same as using the variable to which it points. You can use a dereferenced pointer in an expression in the same way as the original variable, as the expression for the initial value of `price` shows.

It may seem confusing that you have several different uses for the same symbol, `*`. It’s the multiplication operator and the indirection operator, and it’s also used in the declaration of a pointer. The compiler is able to distinguish the meaning of `*` by the context. The expression `*count * *unit_price` may look slightly confusing, but the compiler has no problem determining that it’s the product of two dereferenced pointers. There’s no other meaningful interpretation of this expression. If there was, it wouldn’t compile. You could always add parentheses to make the code easier to read, though: `(*count) * (*unit_price)`.

# Why Use Pointers?

A question that usually springs to mind at this point is “Why use pointers at all?” After all, taking the address of a variable you already know about and sticking it in a pointer so that you can dereference it later seems like an overhead you can do without. There are several reasons pointers are important:

+   - Later in this chapter you’ll learn how to allocate memory for new variables dynamically—that is, during program execution. This allows a program to adjust its use of memory depending on the input. You can create new variables while your program is executing, as and when you need them. When you allocate new memory, the memory is identified by its address, so you need a pointer to record it.
+   - You can also use pointer notation to operate on data stored in an array. This is completely equivalent to the regular array notation, so you can pick the notation that is best suited for the occasion. Mostly, as the name suggests, array notation is more convenient when it comes to manipulating arrays, but pointer notation has its merits as well.
+   - When you define your own functions in Chapter 8, you’ll see that pointers are used extensively to enable a function to access large blocks of data that are defined outside the function.
+   - Pointers are fundamental to enabling *polymorphism* to work. Polymorphism is perhaps the most important capability provided by the object-oriented approach to programming. You’ll learn about polymorphism in Chapter 15.

> **Note**  The last two items in this list apply equally well to references—a language construct of C++ that is similar to pointers in many ways. References are discussed near the end of this chapter.

# Pointers to Type char

A variable of type “pointer to char” has the interesting property that it can be initialized with a string literal. For example, you can declare and initialize such a pointer with this statement:

```
char* proverb { "A miss is as good as a mile"};    // Don't do this!
```