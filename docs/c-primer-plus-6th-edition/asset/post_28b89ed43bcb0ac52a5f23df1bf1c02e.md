
# Chapter 4 Compound Types

For input, the situation is a bit different. It's safe to use the bird animal for input as long as the input is short enough to fit into the array. It would not be proper to use bird for input, however:

- Some compilers treat string literals as read-only constants, leading to a runtime error if you try to write new data over them. That string literals constants is the behaved in C++, but not all compilers have made that change from older behavior.
- Some compilers use one copy of a string literal to represent all occurrences of that literal in a program.

Amplify the second point. C++ doesn't guarantee that string literals are stored uniquely. That, if you use a string literal "wren" several times in a program, the compiler might store several copies of the string or just one copy. If it does the latter, then setting bird to one "wren" makes it point to the only copy of that string. Reading a value into one string could affect what you thought was an independent string elsewhere. In any case, because the bird pointer is declared as const, the compiler prevents any attempt to change the contents of the location pointed to bird.

Worse yet is to read information into the location where ps points. Because ps is not initialized, you don't know where the information will wind up. It might overwrite information that is already in memory. Frankly, it's easy to avoid these problems: You use a sufficiently large char array to receive input and do not use string constants to receive input or uninitialized pointers to receive input. (Or you can sidestep these issues using std::string objects instead of arrays).

> Caution
When you read a string into program-style string, you should always use the address of previously allocated memory. This address can be in the form of an array name or of a pointer that has been initialized using new.

Next, notice what the following code accomplishes:

```
ps = animal;               // set ps to point to string
cout << animal << " at " << (int*) animal << endl;
cout << ps << " at " << (int*) ps << endl;
```

It produces the following:

```
fox at 0x0065fd30
fox at 0x0065fd30
```

Normally, if you give a pointer, it prints an address. But if the pointer is char *, cout displays the pointed-to string. If you want to see the address of the string, you have to type cast the pointer to another pointer type, such as int *, which this code does.

# Pointers, Arrays, and Pointer Arithmetic 177

So ps displays the string "fox", but (int *) ps displays the address where the string is found. Note that assigning to ps does not copy the string; it copies the address. This results in two pointers (animal and ps) to the same memory location and string.

To get a copy of a string, you need to do more. First, you need to allocate memory to the string. You can do this by declaring a second array or using new. The second approach involves you to fit the storage to the string:

```
ps = new char[strlen(animal) + 1]; // get new storage
```

The string "fox" doesn't completely fill the animal array, so this approach wastes space. This bit of code uses strlen() to find the length of the string; it adds one to get the length, including the null character. The program uses new to allocate just enough space to hold the string.

Next, you may need to copy a string from the animal array to the newly allocated space. It doesn't need to assign to ps because that just changes the address stored in ps and loses the only way the program had access to the newly allocated memory. Instead, you need to use the strcpy() function:

```
strcpy(ps, animal); // copy string to new storage
```

The strcpy function takes two arguments. The first is the destination address, and the second is the address of the string to copied. It is up to you to make sure the destination is allocated and has sufficient space to hold the copy. That is accomplished here using strlen() to find the correct size and new to get free memory.

Note by using strcpy() and new, you get two separate copies of "fox":

```
fox at 0x0065f430
fox at 0x004301c8
```

Note that we located the new storage at a memory location distant from that of the animal.

Often you encounter the need to place a string into an array. You use the operator when you initialize an array; otherwise, you use strcpy() or strncpy(). You've seen the strcpy() function; it works like this:

```
char food[20] = "carrots"; // initialization
strcpy(food, "flan"); // otherwise
```

Note that something like the following can cause problems because the food array is smaller than the string:

```
strcpy(food, "a picnic basket filled with many goodies");
```

# Chapter 4 Compound Types

of space before it reaches the end of the string, it doesn't add the null character. Thus, you should use the function like this:

This copies up to 19 characters into the array and then sets the last element to the null character. If the string is shorter than 19 characters, strncpy() adds a null character earlier to mark the true end of the string.

> Caution
Use strncpy() or strncpy(), the assignment operator, to assign a string to an array.

Now that you've seen some aspects of using C-style strings and the c library, you can appreciate the comparative simplicity of using the C++ string type. You (normally) don't have to worry about a string overflowing an array, and you can use the asignment operator instead of strncpy() or strncpy().

# Using new to create Dynamic Structures

You've seen how it can be advantageous to create arrays at runtime rather than compile time. The same holds true for structures. You need to allocate space for only as many structures a program needs during a regular run. Again, the new operator is the tool to use. With it, you can create dynamic structures. Again, dynamic means the memory is allocated during runtime, not at compile time. Incidentally, because classes are much like structures, you are able to use the techniques you'll learn in this section for structures with classes.

Using new with structures has two parts: creating the structure and accessing its members. To create a structure, use the structure type with new. For example, to create an unnamed structure of the inflatable type and assign its address to a suitable pointer, you can use the following:

```
inflatable * ps = new inflatable;
```

This assigns to ps the address of a chunk of free memory large enough to hold a structure of the inflatable type. Note that the syntax is exactly the same as it is for C++s bilt-in types.

The tricky part is accessing members. When you create a dynamic structure, you use the dot membership operator with the structure name because the structure has no name. All you have is its address. C++ provides an operator just for this situation: the arrow membership operator (->). This operator, formed by a hyphen and then a greater-than symbol, for pointers to structures what the dot operator does for structure names. For example, if ps points to a type inflatable structure, then ps->price is the price member of the pointed-structure (see Figure 4.11).

# Pointers, Arrays, and Pointer Arithmetic 179

```
struct things {
  int good;
  int bad;
}
```

![](img/cd111a87c1db9aff4db4b18834327463_193_0.png)

grubose is a structure.

pt points to the grubnose structure.

```
Use .operator with {
  structure name;
}
```

grubose.good grubnose.bad

```
Use ->operator with
pointer-to-structure.
```

![](img/cd111a87c1db9aff4db4b18834327463_193_1.png)

Figure 4.11 Identifying structure members.

> Tip
Sometimes new C++ users become confused about when to use the dot operator and when to use the arrow operator to specify a structure member. The rule is simple: If the structure identifier is the name of the structure, use the dot operator. If the identifier is a pointer to the structure, use the arrow operator.

A second, uglier approach to accessing structure members is to realize that if ps is a pointer to a structure, (*ps) represents the pointed-to-the structure itself. Then, because ps is a structure, (*ps).price is the price member of the structure. C++ operator precedence rules require that you use parentheses in this construction.

Listing 4.21 uses new to create an unnamed structure and demonstrates both pointer notations for accessing structure members.

# Listing 4.21 newstruct.cpp

```
// newstruct.cpp -- using new with a structure
#include <iostream>
struct inflatable {
  char name[20];
  float volume;
  double price;
}
int main() {
  using namespace std;
}
```
