# ESP In Action

![](bbox=[0.148, 0.093, 0.457, 0.497])

#  8.3 ESP In Action

```
```This code example uses MASM Syntax```
```

Let's say we want to discard 3 items we pushed earlier onto the stack, without saving the values (in other words 'clean' the stack). The following works:

```
pop eax
pop eax
pop eax
xor eax, eax ; clear eax because we don't need the values
```

However there is a faster method. We can simply perform some basic arithmetic on esp to make the pointer go "above" the data items, so they cannot be read anymore, and can be overwritten with the next round of push commands.

```
```add esp, 12 ; 12 is 3 DWORDs (4 bytes * 3)```
```