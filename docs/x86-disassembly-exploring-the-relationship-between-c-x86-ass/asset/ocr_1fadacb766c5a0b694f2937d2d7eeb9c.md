# Data Structures

```
void MyFunction()
{
  char buffer[4];
  ...
```

This will translate into the following asm pseudo-code:

```
:_Function2
push ebp
mov ebp, esp
sub esp, 4
lea $buffer, [esp + 0]
```

Which looks harmless enough. But, if a program inadvertently accesses buffer[4]? what about buffer[5]? what about buffer[8]? This is the makings of a buffer overflow vulnerability, and (might) will be discussed in a later section. However, this section won't talk about security issues, and instead will focus on data structures.

# 19.2.1 Spoting an Array on the Stack

To spot an array on the stack, look for large amounts of local storage allocated on the stack ('sub esp, 1000', for example), and look for large portions of that data being accessed by an offset from a different register from esp. For instance:

```
:_Function3
push ebp
mov ebp, esp
sub esp, 256
lea ebx, [esp + 0x00]
mov [ebx + 0], 0x00
```

is a good sign of an array being created on the stack. Granted, an optimizing compiler might just want to offset from esp instead, so you will need to be careful.

# 19.2.2 Spoting an Array in Memory

Arrays in memory, such as global arrays, or arrays which have initial data (remember, initialized data is created in the .data section in memory) and will be accessed as offsets from a hardcoded address in memory:

```
:_Function4
push ebp
mov ebp, esp
mov esi, 0x77651004
mov ebx, 0x00000000
mov [esi + ebx], 0x00
```

It needs to be kept in mind that structures and classes might be accessed in a similar manner, so the reverser needs to remember that all the data objects in an array are of the same type, that they are sequential, and will often be handled in a loop of some sort. Also, that this might be the most important part), each elements in an array may be accessed by a variable offset from the base.

132