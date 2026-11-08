
Now you're nearly getting the best of all possible worlds. You have a one-dimensional array of pointers defined such that the compiler works out the array size from the number of initializing strings. The memory usage that results from this statement is illustrated in Figure 6-4.

![](img/020c376b6cc4874983a4344f51a256de_199_0.png)

*Figure 6-4. An array of pointers*

With the char array of Ex5_11, each row had to have at least the length of the longest string, which resulted in quite some wasted bytes. Figure 6-4 clearly shows that by allocating all strings separately this is no longer an issue in Ex6_04. Granted, you do need some extra memory to store the addresses of the strings, typically 4 or 8 bytes per string pointer. And since in our example the difference in string lengths is not that great yet, we might not actually have gained much yet (on the contrary even).

In general, however, the cost of an extra pointer is often negligible compared to the memory required for the strings themselves. And even for our test program this is not entirely unthinkable. Suppose, for instance, that we'd ask you to add the following name as a ninth option: “Rodolfo Alfonso Raffaello Pierre Filibert Guglielmi di Valentina d'Antonguolla” (which is, we kid you not, the real name of an iconic star of the silent movie era).

Saving space isn't the only advantage that you get by using pointers. In many circumstances, you can save time too. For example, think of what happens if you want to swap “Greta Garbo” with “Mae West” in the array. You'd need to do this to sort the strings into alphabetical order, for example. With the pointer array, you just reorder the pointers—the strings can stay right where they are. With a char array, a great deal of copying would be necessary. Interchanging the string would require the string “Greta Garbo” to be copied to a temporary location, after which you would copy “Mae West” in its place. Then you would need to copy “Greta Garbo” to its new position. All of this would require significantly more execution time than interchanging two pointers. The code using an array of pointers is similar to that using a char array. The number of array elements that is used to check that the selection entered is valid is calculated in the same way.

The extra `const` keyword following the element type specification defines the elements as constant, so now the pointers and strings they point to are defined as constant. Nothing about this array can be changed.

Perhaps we made it a bit too complicated starting you out with an array of pointers. Because it's important that you understand the different options, let's go over things once more using a basic const char variable, pointing to just one celebrity. We'll consider this definition:

```cpp
const char* my_favorite_star{ "Lassie" };
```

This defines a pointer that points to const char elements. This means the compiler will, for instance, not let you rename Lassie to Lossie:

```cpp
my_favorite_star[1] = 'o';    // Error: my_favorite_star[1] is const!
```

The definition of my_favorite_star, however, does not prevent you from changing your mind about which star you prefer. This is because the my_favorite_star variable itself is not const. In other words, you’re free to overwrite the pointer value stored in my_favorite_star, as long as you overwrite it with a pointer that refers to const char elements:

```cpp
my_favorite_star = "Mae West";    // my_favorite_star now points to "Mae West"
my_favorite_star = pstars[1];      // my_favorite_star now points to "Clara Bow"
```

If you want to disallow such assignments, you have to add a second const to protect the content of the my_favorite_star variable:

```cpp
const char* const forever_my_favorite{ "Oliver Hardy" };
```

To summarize, you can distinguish three situations that arise using const when applied to pointers and the things to which they point:

- *A pointer to a constant:* You can’t modify what's pointed to, but you can set the pointer to point to something else:

  ```cpp
  const char* pstring {"Some text that cannot be changed"};
  ```

  Of course, this also applies to pointers to other types. Here’s an example:

  ```cpp
  const int value {20};
  const int* pvalue {&value};
  ```

  Here, value is a constant and can’t be changed, and pvalue is a pointer to a constant, so you can use it to store the address of value. You couldn’t store the address of value in a pointer to non-const int (because that would imply that you can modify a constant through a pointer), but you could assign the address of a non-const variable to pvalue. In the latter case, you would be making it illegal to modify the variable through the pointer. In general, it’s always possible to strengthen const-ness, but weakening it isn’t permitted.

- *A constant pointer:* The address stored in the pointer can’t be changed. A constant pointer can only ever point to the address that it’s initialized with. However, the contents of that address aren’t constant and can be changed. Suppose you define an integer variable and a constant pointer:

  ```cpp
  int data {20};
  int* const pdata {&data};
  ```

  pdata is const, so it can only ever point to data. Any attempt to make it point to another variable will result in an error message from the compiler. The value stored in data isn’t const, though, so you can change it:

  ```cpp
  *pdata = 25;        // Allowed, as pdata points to a non-const int
  ```

  Again, if data was declared as const, you could not initialize pdata with &data. pdata can only point to a non-const variable of type int.

- *A constant pointer to a constant:* Here, both the address stored in the pointer and the item pointed to are constant, so neither can be changed. Taking a numerical example, you can define a variable called value like this:

  ```cpp
  const float value {3.1415f};
  ```

  value is a constant, so you can’t change it. You can still initialize a pointer with the address of value, though:

  ```cpp
  const float* const pvalue {&value};
  ```

  pvalue is a constant pointer to a constant. You can’t change what it points to, and you can’t change what is stored at that address.

> **Tip**  In some rare cases, the need for even more complex types arises, such as pointers to pointers. A practical tip then is that you can read all type names right to left. While doing so, you read every asterisk as “pointer to.” Consider this variant—an equally legal one, by the way—of our latest variable declaration:
>
> ```cpp
> float const* const pvalue {&value};
> ```
>
> Reading right to left then reveals that pvalue is indeed a const pointer to a const float. This trick always works (even when references enter the arena later in this chapter). You can give it a try with the other definitions in this section. The only additional complication is that the first const is typically written prior to the element type.
>
> ```cpp
> const float* const pvalue {&value};
> ```
>
> So when reading types right to left, you often still have to swap around this const with the element type. It shouldn’t be hard to remember, though. After all, “const pointer to float const” just doesn’t have the same ring to it!

## Pointers and Arrays

There is a close connection between pointers and array names. Indeed, there are many situations in which you can use an array name as though it were a pointer. An array name by itself mostly behaves like a pointer when it's used in an output statement, for instance. That is, if you try to output an array by just using its name, you'll just get the hexadecimal address of the array—unless it's a char array, of course, for which all standard output streams assume it concerns a C-style string. Because an array name can be interpreted as an address, you can use one to initialize a pointer as well:

```cpp
double values[10];
double* pvalue {values};
```

This will store the address of the values array in the pointer pvalue. Although an array name represents an address, it is not a pointer. You can modify the address stored in a pointer, whereas the address that an array name represents is fixed.

### Pointer Arithmetic

You can perform arithmetic operations on a pointer to alter the address it contains. You're limited to addition and subtraction for modifying the address contained in a pointer, but you can also compare pointers to produce a logical result. You can add an integer (or an expression that evaluates to an integer) to a pointer, and the result is an address. You can subtract an integer from a pointer, and that also results in an address. You can subtract one pointer from another, and the result is an integer, not an address. No other arithmetic operations on pointers are legal.

Arithmetic with pointers works in a special way. Suppose you add 1 to a pointer with a statement such as this:

```cpp
++pvalue;
```

This apparently increments the pointer by 1. Exactly *how* you increment the pointer by 1 doesn't matter. You could use an assignment or the += operator to obtain the same effect so that the result would be exactly the same with this statement:

```cpp
pvalue += 1;
```

The address stored in the pointer *won't* be incremented by 1 in the normal arithmetic sense, however. Pointer arithmetic implicitly assumes that the pointer points to an array. Incrementing a pointer by 1 means incrementing it by one *element* of the type to which it points. The compiler knows the number of bytes required to store the data item to which the pointer points. Adding 1 to the pointer increments the address by that number of bytes. In other words, adding 1 to a pointer increments the pointer so that it points to the next element in the array. For example, if pvalue is a pointer to double and type double is 8 bytes, then the address in pvalue will be incremented by 8. This is illustrated in Figure 6-5.
