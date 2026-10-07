# Chapter 4 Compound Types

```
using namespace std;
inflatable guests[2] = // initializing an array of structs
{
    "Bambi", 0.5, 21.99;
    "Godzilla", 2000, 565.99 // next structure in array
};
```

```
cout << "The guests " << guests[0].name << " and " << guests[1].name
    << "nhave a combined volume of "
    << guests[0].volume + guests[1].volume << " cubic feet.\n";nreturn 0;
```

Here is the output of the program in Listing 4.13:

The guests Bambi and Godzilla
have a combined volume of 2000.5 cubic feet.

# Bit Fields in Structures

C++, like C, enables you to specify structure members that occupy a particular number of bits. This can be handy for creating a data structure that corresponds, say, to a register on hardware device. The field type should be an integral or enumeration (enumeration discussed later in this chapter), and a colon followed by a number indicates the actual number of bits to be used. You can use unnamed fields to provide spacing. Each member is termed a *bit field*. Here's an example:

```
struct torge_register{
    unsigned int SN : 4; // 4 bits for SN value
    unsigned int : 4; // 4 bits unused
bool goodIn : 1; // valid input (1 bit)
bool goodToggle : 1; // successful toggling
};
```

You can initialize the fields in the usual manner, and use standard structure notation to access bit fields:

```
torge_register tr = { 14, true, false };
```

```
if (tr.goodIn) // if statement covered in Chapter 6
```

Bit fields are typically used in low-level programming. Often, using an integral type and the bitwise operators used in Appendix E,"Other Operators," provides an alternative approach