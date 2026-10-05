# MEMORY MANAGEMENT FUNCTIONS

This section discusses briefly the memcpy(), memmove(), and memcmp() functions that are often used for memory management. memcpy() is used to copy any type of data from one memory region to another. It is declared in cstring:

```
void *memcpy(void *dest, const void *src, size_t size);
```

memcpy() copies bytes from the memory pointed to by src to the destination pointed by dest. If the source and destination addresses overlap, its behaviour is undefined. For example, the following code allocates memory for "ABCDE" string in it:

```
char *arr = new char[6]; // Allocate one extra byte for the null character.
memcpy(arr, "ABCDE");
```

The main difference with strcpy() is that strcpy() stops copying when the null character is. On the other hand, memcpy() does not stop copying until the number of specified bytes are filled. For example, if we:

```
char str2[6], str1[] = {'a', 'b', 'c', '\0', 'd', 'e'};
```

and write: memcpy(str2, str1, 6);
the content of str2 would be the same as str1.

On the other hand, if we write: strcpy(str2, str1);
t content of str2 would be: {'a', 'b', 'c', '\0'}.

memmove() is similar to memcpy(), except that memmove() guarantees that the data will be copied correctly even if source and destination memory overlap. Because memcpy() does not check if the two memory regions overlap, it executed after memmove(). Notice that the size of the destination memory be size bytes, at least. If the extra bytes would be written in a non-allocated memory, which means that the existing data will be overwritten. For example, the next copy is wrong because the size of the destination memory is 3 bytes, while the copied bytes are:

```
char str1[3], str2[] = "abcde";
memcpy(str1, str2, sizeof(str2)); // Be careful.
```

> memcpy() is very useful, because it is implemented in a way that copying blocks of data is practically faster than an iteration loop.

For the example, the following code uses memcpy() to copy any array to another:

```
int arr1[SIZE], arr2[SIZE];
memcpy(arr2, arr1, sizeof(arr1)); /* We use memcpy() instead of an iteration
loop such as:
  for(int i = 0; i < SIZE; i++)
    arr2[i] = arr1[i]; */
```