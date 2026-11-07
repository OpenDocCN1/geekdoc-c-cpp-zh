is the last element set to c. The reason for filling the string from back to front instead of front to back is to avoid using an additional variable. Using the other order would involve something like this:

```
int i = 0;
while (i < n)
    pstr[i++] = c;
```

Note that the variable pstr is local to the buildstr function, so when that function terminates, the memory used for pstr (but not for the string) is freed. But because the function returns the value of pstr, the program is able to access the new string through the ps pointer in main().

The program in Listing 7.10 uses delete to free memory used for the string after the string is no longer needed. Then it reuses ps to point to the new block of memory obtained for the next string and frees that memory. The disadvantage to this kind of design (having a function return a pointer to memory allocated by new) is that it makes it the programmer’s responsibility to remember to use delete. In Chapter 12, “Classes and Dynamic Memory Allocation,” you’ll see how C++ classes, by using constructors and destructors, can take care of these details for you.

# Functions and Structures

Let’s move from arrays to structures. It’s easier to write functions for structures than for arrays. Although structure variables resemble arrays in that both can hold several data items, structure variables behave like basic, single-valued variables when it comes to functions. That is, unlike an array, a structure ties its data in to a single entity, or data object, that will be treated as a unit. Recall that you can assign one structure to another. Similarly, you can pass structures by value, just as you do with ordinary variables. In that case, the function works with a copy of the original structure. Also a function can return a structure. There’s no funny business like the name of an array being the address of its first element. The name of a structure is simply the name of the structure, and if you want its address, you have to use the & address operator. (C++ and C both use the & symbol to denote the address operator. C++ additionally uses this operator to identify reference variables, to be discussed in Chapter 8.)

The most direct way to program by using structures is to treat them as you would treat the basic types—that is, pass them as arguments and use them, if necessary, as return values. However, there is one disadvantage to passing structures by value. If the structure is large, the space and effort involved in making a copy of a structure can increase memory requirements and slow down the system. For those reasons (and because, at first, C didn’t allow the passing of structures by value), many C programmers prefer passing the address of a structure and then using a pointer to access the structure contents. C++ provides a third alternative, called passing by reference, that is discussed in Chapter 8. Let’s examine the other two choices now, beginning with passing and returning entire structures.