you’re in for some technical differences. The following lines of code show these differences. First, think about what happens if you initialize a two-dimensional array of characters like this:

```
char NameArray[ ][6] = {
    {'T', 'o', 'm', '\0', '\0', '\0'},
    {'S', 'u', 'z', 'y', '\0', '\0'},
    {'H', 'a', 'r', 'r', 'y', '\0'}
};
```

This is an array of an array. Each inner array is an array of six characters. The *outer* array stores the three inner arrays. (The individual content of an array is sometimes called a *member* — the inner array has six members and the outer array has three members.) Inside memory, the 18 characters are stored in one consecutive row, starting with T, then o, and ending with y and finally \0, which is the null character.

But now take a look at this:

```
char* NamePointers[] = {
    "Tom",
    "Suzy",
    "Harry"
};
```

This is an array of character arrays as well, except that it’s not the same as the code that came just before it. This is actually an array holding three pointers: The first points to a character string in memory containing Tom (which is followed by a null-terminator, \0); the second points to a string in memory containing Suzy ending with a null-terminator; and so on. Thus, if you look at the memory in the array, you won’t see a bunch of characters; instead, you see three numbers, each being a pointer.

![](bbox=[0.153, 0.643, 0.229, 0.717])

It’s often helpful to see the content of memory as you work with arrays. To see memory in Code::Blocks, choose Debug→Debugging Windows→Memory Dump. You see the Memory window. Type &(ampersand) plus the name of the variable you want to view in the Address field and click Go. (You can also see the content of a specific memory address by typing its address, such as **0x28ff08**, or the memory pointed to by a register by typing $ plus the register name, such as **$sp**.)

![](bbox=[0.153, 0.779, 0.229, 0.847])

So where on earth (or in the memory, anyway) are the three strings, Tom, Suzy, and Harry when you have an array of three pointers to these strings? When the compiler sees string constants such as these, it puts them in a special area where it stores all the constants. These constants then get added to the executable file at link time, along with the compiled code for the source module. (For information on linking, see Appendix A.) And that’s where they reside in memory. The array, therefore, contains pointers to these three constant strings in memory.