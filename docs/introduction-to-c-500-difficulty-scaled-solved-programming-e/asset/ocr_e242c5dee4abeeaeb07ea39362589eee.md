# 376 Introduction to C++

Bit fields are often used for the description and access of information encoded in bit level, such as the hardware registers. For example, of the register depicted in the following figure could be encoded like this: 

| bit8 | bit7 | bit6 | bit5 | bit4 | bit3 | bit2 | bit1 |
|---|---|---|---|---|---|---|---|n| S | Z | | AC | | P | CS |

```
struct Flags_Reg
{
    unsigned int cs : 1;
    unsigned int p : 1;
    unsigned int ac : 1;
    unsigned int z : 1;
    unsigned int s : 1;
};
```

An alternative way to handle the register is to use bit operators as we did in C.4.7. Using the above, it is much easier to handle the register and assign values to its fields. For example, if we have a Flags_Reg variable (e.g., fr), to access the ac field we can write:
unsigned int ac = fr.ac; while if we use an integer to represent the register value (e.g., reg) and manipulate the bits as in Chapter 4 we should write:
unsigned int ac = (reg >> 4) & 1;

The former syntax makes the code clearer and easier to read. However, as we'll see later, if we want our program to be portable, it is better to use bit operators, so that it won't depend on how the compiler allocates the bits.
A field might be unnamed. Unnamed fields are typically used for padding. For example, to represent the exact form of the register above, we could add three unnamed fields:

```
struct Flags_Reg
{
    unsigned int cs : 1;
    unsigned int p : 1;
    unsigned int ac : 1;
    unsigned int : 1;
    unsigned int : 1;
    unsigned int s : 1;
};
```

The bit fields are packed into storage units (its typical size is 32 bits). To force the compiler to store a bit field at the beginning of the next unit, a field of zero length is added before that. For example, in the following structure, if the compiler uses a storage unit of 32-bit, it will allocate three bits for the f field, skip the next 29 bits to the next unit, and allocate four more bits for the k field.

```
struct Test
{
    unsigned int f : 3;
    unsigned int : 0;
    unsigned int k : 4;
};
```