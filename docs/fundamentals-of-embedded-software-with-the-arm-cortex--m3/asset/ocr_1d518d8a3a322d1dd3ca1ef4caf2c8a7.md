# 6.6.2 Translating C Subscript Expressions to Assembly

A subscripted array reference shares much in common with pointer dereferencing. In either case, the address calculation involves three components:

+   1. The starting address (provided either by a pointer or by the name of an array)
+   2. The value of a subscript or integer offset
+   3. The size of the objects held in the array or pointed to by the pointer

The only real difference is whether the starting address is a constant or a variable. In fact, you can actually subscript a pointer or dereference an array name.3 Consider the declarations:

```
int32_t array[100], *ptr2word, k ;
```

Applying a subscript to the pointer (e.g., ptr2word[k] = 0;) produces the same ARM assembly code we saw earlier for “*(ptr2word+k) = 0,” and dereferencing the array name (e.g., “*(array + k) = 0;”) is equivalent to the subscripted reference array[k] = 0, which produces very similar assembly code:

```
LDR R0,=0 ;get the constant zero
ADR R1,array ;get the starting address of “array”
LDR R2,k ;get the integer held in “k”
STR R0,[R1,R2,LSL#2] ;store at address 4k bytes into array
```

# 6.6.3 Translating Structure References to Assembly

The location of a member element within a structure is obtained by adding a constant (10 in the examples below) to the starting address of the structure. When the reference is specified using the name of a global or statically allocated structure, as in

```
s.m = 5 ; ;store 5 into member 'm' of structure 's'
```

then the address of the member element is the sum of two constants and may be computed when the code is assembled:

```
LDR R0,=5 ;get the constant 5
STR R0,s+10 ;store 5 into the member element
```

However, if the reference to the structure is via a pointer, as in

```
p->m = 5 ; ;store 5 into member 'm' of the structure pointed to by 'p'
```

then the address must be calculated at run-time using the value of the pointer:

```
LDR R0,=5 ;get the constant 5
LDR R1,p ;get the address of the structure from the pointer
STR R0,[R1,#10] ;store 5 into the member element
```