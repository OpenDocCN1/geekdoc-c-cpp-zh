
If we're lucky, the relevant parts of the program check how much of an array they've used, and print an error message or otherwise gracefully abort before overflowing the array. If we're not so lucky, a program may sail off the end of an array, overwriting other data and behaving quite badly. In either case, the user doesn't get his job done. How can we avoid the restrictions of fixed-size arrays?

The answers all involve the standard library function malloc. Very simply, malloc returns a pointer to n bytes of memory which we can do anything we want to with. If we didn't want to read a line of input into a fixed-size array, we could use malloc, instead. It takes the following form:

```c
ptr=(cast-type*)malloc(byte-size)
```

where ptr is a pointer of type cast-type. The malloc returns a pointer (of cast-type) to an area of memory with size byte-size.

Here is an example

```c
#include <stdlib.h>
char *line;
int linelen = 100;
line = (char *)malloc(linelen);
/* incomplete -- malloc's return value not checked */
getline(line, linelen);
```

malloc is declared in <stdlib.h>, so we #include that header in any program that calls malloc. A “byte" in C is, by definition, an amount of storage suitable for storing one character, so the above invocation of malloc gives us exactly as many chars as we ask for. We could illustrate the resulting pointer like this:

![](img/43e13c54e7f7445669b8794c025df636_276_0.png)

The 100 bytes of memory (not all of which are shown) pointed to by line are those allocated by malloc. (They are brand-new memory, conceptually a bit different from the memory which the compiler arranges to have allocated automatically for our conventional variables. The 100 boxes in the figure don't have a name next to them, because they're not storage for a variable we've declared.)

As a second example, we might have occasion to allocate a piece of memory, and to copy a string into it with strcpy:

```c
char *p = (char *)malloc(15);
```

```c
/* incomplete -- malloc's return value not checked */
strcpy(p,"Hello, world!");
```

When copying strings, remember that all strings have a terminating \0 character. If you use strlen to count the characters in a string for you, that count will not include the trailing \0, so you must add one before calling malloc:

```c
char *somestring, *copy;
...
copy = (char *)malloc(strlen(somestring) + 1); /* +1 for \0 */
/* incomplete -- malloc's return value not checked */
strcpy(copy, somestring);
```

What if we're not allocating characters, but integers? If we want to allocate 100 ints, how many bytes is that? If we know how big ints are on our machine (i.e. depending on whether we're using a 16- or 32-bit machine) we could try to compute it ourselves, but it's much safer and more portable to let C compute it for us. C has a sizeof operator, which computes the size, in bytes, of a variable or type. It's just what we need when calling malloc. To allocate space for 100 ints, we could call

```c
int *ip =(int *)malloc(100 * sizeof(int));
```

The use of the sizeof operator tends to look like a function call, but it's really an operator, and it does its work at compile time.

Since we can use array indexing syntax on pointers, we can treat a pointer variable after a call to malloc almost exactly as if it were an array. In particular, after the above call to malloc initializes ip to point at storage for 100 ints, we can access ip[0], ip[1], ... up to ip[99]. This way, we can get the effect of an array even if we don't know until run time how big the “array" should be. (In a later section we'll see how we might deal with the case where we're not even sure at the point we begin using it how big an “array" will eventually have to be.)

Our examples so far have all had a significant omission: they have not checked malloc's return value. Obviously, no real computer has an infinite amount of memory available, so there is no guarantee that malloc will be able to give us as much memory as we ask for. If we call malloc(100000000), or if we call malloc(10) 10,000,000 times, we're probably going to run out of memory.

When malloc is unable to allocate the requested memory, it returns a null pointer. A null pointer, remember, points definitively nowhere. It's a “not a pointer" marker; it's not a pointer you can use. Therefore, whenever you call malloc, it's vital to check the returned pointer before using it! If you call malloc, and it returns a null pointer, and you go off and use that null pointer as if it pointed somewhere, your program probably won't last long. Instead, a program should immediately check for a null pointer, and if it receives one, it should at the very least print an error message and exit, or perhaps figure out some way of proceeding without the memory it asked for. But it cannot go on to use the null pointer

it got back from malloc in any way, because that null pointer by definition points nowhere. (“It cannot use a null pointer in any way” means that the program cannot use the `*` or `[]` operators on such a pointer value, or pass it to any function that expects a valid pointer.) A call to malloc, with an error check, typically looks something like this:

```c
int *ip = (int *)malloc(100 * sizeof(int));

if(ip == NULL)
{
    printf("out of memory\n");
    exit or return
}
```

After printing the error message, this code should return to its caller, or exit from the program entirely; it cannot proceed with the code that would have used ip.

Of course, in our examples so far, we’ve still limited ourselves to “fixed size” regions of memory, because we’ve been calling malloc with fixed arguments like 10 or 100. (Our call to getline is still limited to 100-character lines, or whatever number we set the linelen variable to; our ip variable still points at only 100 ints.) However, since the sizes are now values which can in principle be determined at run-time, we’ve at least moved beyond having to recompile the program (with a bigger array) to accommodate longer lines, and with a little more work, we could arrange that the “arrays” automatically grew to be as large as required. (For example, we could write something like getline which could read the longest input line actually seen).

### 12.2.2 Allocating memory with calloc

calloc is another memory allocation function that is normally used for requesting memory space at run time for storing derived data types such as arrays and structures. While malloc allocates a single block of storage space, calloc allocates multiple blocks of storage, each of the same size, and then sets all bytes to zero. The general form of calloc is:

```c
ptr=(cast-type *)calloc(n, elem-size);
```

The above statement allocates contiguous space for n blocks, each of size elem-size bytes. All bytes are initialized to zero and a pointer to the first byte of the allocated region is returned. If there is not enough space, a NULL pointer is returned.

### Program 12.1 Program to illustrate the use of malloc and calloc functions

```c
#include <stdio.h>
#include <malloc.h>
main()
{
int *base;
int i;
int cnt=0;
int sum=0;
printf("how many integers you have to store \n");
scanf("%d",&cnt);
base = (int *)malloc(cnt * sizeof(int));
printf("the base of allocation is %16lu \n",base);
if(!base)
printf("unable to allocate size \n");
else
{
for(int j=0;j<cnt;j++)
*(base+j)=5;
}
sum = 0;
for(int j=0;j<cnt;j++)
sum = sum + *(base+j);
printf("total sum is %d\n",sum);
free(base);
printf("the base of allocation is %16lu \n",base);
base = (int *)malloc(cnt * sizeof(int));
printf("the base of allocation is %16lu \n",base);
base = (int *)malloc(cnt * sizeof(int));
printf("the base of allocation is %16lu \n",base);
base = (int *)calloc(10,2);
printf("the base of allocation is %16lu \n",base);
}
```

### 12.2.3 Freeing Memory

Memory allocated with malloc lasts as long as you want it to. It does not automatically disappear when a function returns, as automatic variables do, but it does not have to remain for the entire duration of your program, either. Just as you can use malloc to control exactly when and how much memory you allocate, you can also control exactly when you deallocate it.

In fact, many programs use memory on a transient basis. They allocate some memory, use it for a while, but then reach a point where they don't need that particular piece any more. Because memory is not inexhaustible, it's a good idea to deallocate (that is, release or free) memory you're no longer using.
