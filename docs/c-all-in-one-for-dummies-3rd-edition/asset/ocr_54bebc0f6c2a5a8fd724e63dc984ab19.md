is ambiguous if something is a pointer to an integer: Is it an array, or is it a single number? The designers of C++ knew this was a problem, so they unam-biguated it. They declared and proclaimed that delete shall only delete a single member. Then they invented a little extra that must have given the compiler writers a headache: They said that if you want to delete an array instead, just throw on an opening and closing bracket after the word delete. And all will be good.

All this stuff about pointers and arrays raises an interesting question: How do you specify a pointer to an array? Well, remember that if you have a line like this

![](bbox=[0.095, 0.26, 0.205, 0.36])

```
```cpp
int LotsOfNumbers[50];
```
```

LotsOfNumbers is really a pointer to an integer — it points to the first position in the array. So, in that regard, you already have a pointer to an array. In fact, if you were to write a function declared with a header like this

```
```cpp
int AddUp(int Numbers[], int Count) {
```
```

and look at the generated assembly code, you would see that the Numbers array really does get passed in as a pointer. To view the disassembly in Code::Blocks, create a breakpoint, start the debugger by pressing F8, and choose Debug→Debugging Windows→Disassembly. Code::Blocks displays the Disassembly window, which contains an assembler view of the code.

So the real question is this: When you have an array, how do you *not* use a pointer with it? The answer? You don't! C++ simply does not have a fundamental array type. Other languages do (Pascal, for example), but C and C++ don't. Yet, even though that's the case, the compiler does have a basic feel for the brackets and does seem to understand arrays. Strange but true.

# ### Storing arrays of pointers and arrays of arrays

Because of the similarities between arrays and pointers, you are likely to encounter some strange notation. For example, in main() itself, we have seen both of these at different times:

```
```cpp
char **argc
char *argv[]
```
```

If you work with arrays of arrays and arrays of pointers, the best bet is to make sure that you completely understand what these kinds of statements mean. Remember that although you can treat an array name as a pointer,