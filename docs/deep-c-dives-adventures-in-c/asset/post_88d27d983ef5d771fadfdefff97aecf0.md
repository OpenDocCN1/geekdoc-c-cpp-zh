
# The Array At The End Of The Struct

The key thing about a struct is that its size has to be known so that a suitable block of memory can be allocated for its storage. What this means is that any field in a struct has to have a known size. When you allocate a string field it has to be to a fixed size string. The same holds for an array and you cannot allocate a VLA within a struct.

This is all true, but there are times when you need to create a struct with an array of a size that can vary. How to do this is obvious. Any array allocated at the end of the struct doesn't affect the layout of the struct and as such you can change its size at any time without disturbing the rest of the struct.

Originally, the accepted trick was to include a zero-length array at the end of the struct:

```c
struct test {
  char c;
  int i;
  int myArray[0];
};
```

but after C99 the correct way to do this is to specify an incomplete array declaration as in:

```c
struct test {
  char c;
  int i;
  int myArray[];
};
```

To make use of the array at the end you simply allocate more memory than the size of the struct which doesn't include any allowance for the array and some additional bytes for the array to use.

```c
struct test *myStruct = malloc(sizeof(test) + sizeof(int[size]));
```

with this allocation you can now write:

```c
myStruct->myArray[i]
```

with $i$ between $0$ and $size-1$.

Notice that it is up to you to allocate the memory needed to extend the struct and it is up to you to make sure that the index stays within the allocated area.

If the idea of including an array at the end of a struct seems an uncommon requirement it is worth pointing out that the array is just another uncommitted area of memory and as such can be cast to whatever you like – including another struct. Using an array in this way is far more common than you might think and it is an idea worth keeping in mind.

## Final Thoughts

In many ways the C struct is the key data structure in C and it is so much more than just an implementation of a data record found in other languages. It is central to the idea that C deals with bits as it is structs that let you determine what the bits mean. This is obvious to any programmer using C for the sort of tasks it was designed for – systems programming and hardware programming. Unfortunately, this is not a view shared by the programmers on the standards committees and the compiler writers, who in the main strive to make C look like a modern language and try to make it easier to optimize the code. This goes against the low-level appeal of structs and type punning in general and even makes them seem undesirable and dangerous.

For a fuller discussion, see Dive 16 which deals with the scandal of undefined behavior.

# Dive 15

## The Union

> “*Form follows function - that has been misunderstood. Form and function should be one, joined in a spiritual union.*”
>
> Frank Lloyd Wright

The union is a special type of struct that is more or less dedicated to the idea of type punning. Its very existence in the C language is a strong indication that type punning is not an accidental feature.

## Union Basics

A union is declared in the same way as a struct, but memory is only allocated for the largest of the union's fields. That is, all of the fields of a union share the same memory. This sounds like a crazy thing to do until you notice that it gives you a way of working with the same bit pattern with different interpretations. You can treat the same area of memory as different types simply by using the appropriate field name. That is, using unions allows you to do reasonably well-defined type punning in C.

The syntax for a union is the same as for a struct, but you replace struct with union. For example:

```c
union {
    int I;
    float F;
} myUnion;
```

This allocates four bytes – assuming sizeof(int) and sizeof(float) are both 4 – that can be used to store an int or a float. Which is stored depends on the field name used to access the union, I or F.

Now you can store an int in the union using:

```c
myUnion.I = 42;
```

or a float using:

```c
myUnion.F = 42.0;
```

In the first case, the bit pattern that represents 42 is stored in the four bytes and in the second, the bit pattern that represents 42.0 is stored in the same four bytes. Of course, there is nothing stopping you from storing an int and reading back a float, or vice versa. This is how the type punning occurs when you use a union.

In principle, you can pun any types, but there is a rule in C, but not C++, that it is legal to read a union member as long as it is not larger than the member most recently written. This is a perfectly reasonable restriction, but even so I can invent, admittedly unlikely, examples of reading a larger type when a smaller type has just been written, but they are all very machine-dependent. This means that, in most cases, you can use union type punning to avoid the compiler warning messages and potential undefined behavior.

As with structs and type punning, you have to take padding into account. To revisit the example in the previous chapter:

```c
struct test1 {
char c;
int i;
};

struct test2{
char c[4];
char i[4];
};

union {
struct test1 myStruct1;
struct test2 myStruct2;
} myUnion;
```

In this case, for a 64-bit machine, struct test1 is padded so that int i is on a word boundary and this means there are three padding bytes between c and i. What this means is that union of the two structs, myUnion, has struct test1.c in struct test2.c[0] and struct test1.i in struct test2.i[0] to struct test2.i[3].

## Color

For a more realistic example of a union, consider the way most graphics hardware stores an ARGB (Alpha, Red, Green, Blue) value in a 32-bit unsigned int. If you want to access each of these bytes, and also treat all four bytes as a single value, then the best way is to define a union:

```c
union Pixel{
struct {unsigned char b,g,r,a};
uint32_t value;
};
```

The only complication is that the order has to be changed to allow for the way x86 stores multiple bytes in a 32-bit word. Notice the order is machine-dependent and for Intel and Arm processors corresponds to "little endian". You can see that the union is of a struct with four byte fields and a single 32-bit word. The four byte fields share the same memory block as the 32-bit word and on 64-bit machines no padding is needed.

Now you can declare a pixel and use it as follows:

```c
union Pixel pixel;
pixel.r = 1;
pixel.g = 255;
pixel.b = 128;
pixel.a = 255;
printf("%d\n", pixel.value);
```

You can see that how you access the union depends on the fields that you specify. If you specify `pixel.r` then you simply work with the first byte of the memory block. If you specify `pixel.value` you work with all four bytes as a single int. There’s no need to cast, simply use the fields that make up the union and you access the memory according to the type.

The type punning version of the pixel union is:

```c
struct Pixel{
    unsigned char b,g,r,a;
};
struct Pixel pixel;
pixel.r = 1;
pixel.g = 255;
pixel.b = 128;
pixel.a = 255;
printf("%d\n",(uint32_t)pixel);
```

A union can often be used in place of type punning, but it often requires a little more pre-planning to alias the fields of a suitable union. It is more difficult to use a union to extend structs as shown earlier because of the way a union changes the way fields are named.

## Type Punning Unions

It is a little-used fact that you can cast a union to a struct or to anything else for that matter. Why not? After all, a union is just a block of memory associated with a number of different types. The block of memory is big enough to hold the largest of the types taking into account any padding that is needed. As a block of memory you can cast it to whatever you want to – but it might not make much sense.

For example:

```c
union Pixel{
    struct {unsigned char b,g,r,a;};
    int value;
};
union Pixel pixel={1,255,128,255};

char (*color)[4];
color=(char *) &pixel;
```
