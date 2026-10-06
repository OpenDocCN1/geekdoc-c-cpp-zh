
```
push	ecx
; Line 11
mov	eax, DWORD PTR tv64[ebp]
mov	DWORD PTR tv64[ebp], eax
mov	eax, DWORD PTR tv64[ebp]
sub	cx, 1
mov	eax, DWORD PTR tv64[ebp]
mov	DWORD PTR tv64[ebp], 3
ja	SHORT $L810
mov	eax, DWORD PTR tv64[ebp]
mov	DWORD PTR $L818[esp+4]
jmp
$L806:	1
; Line 14
push	push
call	_MyFunction
add	esp, 4
; Line 15
jmp	SHORT $L803
$L807:	2
; Line 17
push	push
call	_MyFunction
add	esp, 4
; Line 18
jmp	SHORT $L803
; Line 19
push	3
call	_MyFunction
add	esp, 4
; Line 20
jmp	SHORT $L803
$L809:	4
; Line 22
push	4
call	_MyFunction
add	esp, 4
; Line 23
jmp	SHORT $L803
$L810:	5
; Line 25
push	5
call	_MyFunction
add	esp, 4
$L803:
; Line 27
xor	eax, eax
; Line 28
mov	esp, ebp
pop	ebp
ret	0
$L818:
DD	$L806
DD	$L807
DD	$L808
DD	$L809
_main	ENDB
```

Lets work our way through this. First, we see that line 10 sets up our standard stack frame, and it also saves ecx. Why does it save ecx? Scanning the function, we never see a corresponding 'pop ecx' instruction, so it seems that the value is never restored at all. In fact, the compiler isn't saving ecx at all, but is simply reserving space on the stack: it's creating a local variable. The original C code didn't have any local variables, however, so perhaps the compiler needed some extra scratch space to store intermediate values. Why doesn't the compiler execute the more familiar 'sub esp, 4' command to create the local variable? push ecx is a faster instruction that does the same thing. 'scratch space' is being referenced by a negative offset from ebp. tv64 was defined in the beginning of the listing as having the value -4, so every call to 'tv64[ebp]' is a call to scratch space.

There are a few things that we need to notice about the function in:

- $L803 is the end_of_switch label. Therefore, 'jmp SHORT $L803' statement is a break. This is verifiable by comparing with the C code line-by-line.
- $L818 contains a list of hard-coded memory addresses, where here are labels in the code section! Remember, labels resolve to the memory address of the instruction. This will be an important part of our puzzle.

To solve this, we will take an in-depth look at line 11:

```
mov     DWORD PTR _arg0[ebp], eax
mov     DWORD PTR tv64[ebp], eax
mov     ecx, tv64[ebp]
sub     ecx, 1
mov     DWORD PTR tv64[ebp], ecx
cmp     ecx, $L810
ja     SHORT $L810
mov     edx, DWORD PTR L818[ebx]
jmp     DWORD PTR L818[edx+4]
```

This sequence performs the following pseudo-C operation:

```
if (arg0 - 1 > 4 )
{
    /* the default */
    goto L810;
}
label *L818[] = { $L806, $L807, $L808, $L809 }; /* define a table
of jumps, one per case * */
//
goto L818[arg0 - 1]; /* use the address from the table to jump to
the correct case */
```

Here's why...

## 13.4.1 The Setup

```
mov     eax, DWORD PTR _arg0[ebp]
mov     DWORD PTR tv64[ebp], eax
mov     ecx, DWORD PTR tv64[ebp]
sub     ecx, 1
mov     DWORD PTR tv64[ebp], ecx
```

The value of ecx is moved into eax. The value of the scratch space is then moved into ecx. Like an awfully convoluted way to get the same value into many different locations, but remember: I turned off the optimizations. The value of ecx is then decremented by 1. Why didn't the compiler use a dec instruction instead? Perhaps the statement is a general statement, that in this just happens to have an argument of 1. We don't know exactly, all we know this is:

- eax = "scratch pad"

## Branches

- ecx = eax - 1

Finally, the last line moves the new, decremented value of ecx back into the scratch pad. Very inefficient.

## 13.4.2 The Compare and Jumps

```
cmp     DWORD PTR tv64[ebp], 3
ja     SHORT $L810
```

The value of the scratch pad is compared with the value 3, and if the unsigned value is above 3 (4 or more), execution jumps to $L810 because ja is an unconditional jump. Let's look back at the original C code:

```
switch(argc)
  case 1:
    MyFunction(1);
    break;
  case 2:
    MyFunction(2);
    break;
  case 3:
    MyFunction(3);
    break;
  case 4:
    MyFunction(4);
    break;
  default:
    MyFunction(5);
```

Remember, the scratch pad contains the value (argc - 1), which means that this condition is only triggered when argc > 4. What happens when argc is greater than 4? The function goes to the default. Now, let's look at the next two lines:

```
mov     edx, DWORD PTR tv64[ebp]
jmp     DWORD PTR L818[edx+4]
```

edx gets the value of the scratch pad (argc - 1), and then there is a jump that takes place: execution jumps to a location pointed to by (argc * 4 + $L818). What is $L818?

## 13.4.3 The Switch Table

```
$L818:
DD	$L806
DD	$L807
DD	$L808
DD	$L809
```

$L818 is a pointer, in the code section, to a list of other pointers. These pointers are all 32-bit values (DWORD). Let's look back at our jump:

```
jmp DWORD PTR L818[edx*4]
```

## Ternary Operator

In this jump, $L818 isnt the offset, it's the base, edx*4 is the offset. As we said earlier, edx contains the value (argc - 1). If argc == 1, we jump to [$L818 + 0] which is $L806. If argc == 2, we jump to [$L818 + 4] which is $L807. A look at labels $L806, $L807, $L808, and $L809 shows exactly what we expect: the case statements from the original code, each of the case statements calls "MyFunction", then breaks, and jumps to the end of the switch.

## 13.5 Ternary Operator

Again, the best way to learn is by doing. We will go through a mini example to explain the ternary operator. Consider the following C code:

```
int main(int argc, char **argv)
{
    return (argc > 1) ? 5 : (0);
}
```

cl.exe produces the following assembly:

```
_argc = 0              ; size = 4
_argv = 1             ; size = 4
_main
    PROC NEAR
; C:\documents\andrew\test2.c
    Line 2
    push                ebp
    mov                 eax, esp
    Line 3
    xor                 eax, eax
    cmp                 DWORD PTR [ebp], 1
    setle              al
    and                 eax, 5
    Line 4
    pop                 ebp
    ret
    ret                 0
_main                ENDP
```

Line 2 sets up a stack frame, and line 4 is a standard exit sequence. There are no local variables is where we want to look. The instruction "xor eax, eax" simply sets eax to 0. For more information on that line, see the chapter on intuitive instructions!. The function tests the condition of the ternary operator. The cmp instruction is a set of x86 functions that works like a conditional move: it gets the value if argc < 1. Isn't the exact opposite of what we wanted? In this case, let's look at what happens when argc == 0: al gets the value 1. al is decremented (al = eax), and eax is logically anded with 5. 5 & 0 = 0. When argc == 2 (greater than 1), the function doesn't do anything, and eax still is zero. eax then decremented, which means eax == -1. What is -1?

In x86 processors, negative numbers are stored in two's complement format. For instance, let's look at the following C code:

## Branches

```
BYTE x;
x = -1;
```

At the end of this C code, x will have the value 1111111: all ones!

When argc is greater than 1, let sets al to zero. Decrementing this value sets every bit in eax to a 1. Now, when we perform the logic and function we get:

```
...11111111
&.0000101    ;101 is 5 in binary
----------------
.00000101
```

eax gets the value 5. In this case, its a roundabout method of doing it, but as a reverser, for reference, here is the GCC assembly output of the same ternary operator from above:

```
_main:
pushl  ebp
movl   %esp,ebp
subl   $0,%eax
xorl   eax,eax
andl   $-16,%eax
call   _malloc
call   __main
xorl   %edx,edx
movel   eax,edi
cmpl   $2(%ebp)
setge  dl
leal   (edx,%edx,4),eax
leave
ret
```

Notice that GCC produces slightly different code than cl.exe produces. However, the stack frame is set by us line numbers, or other hints in the code. The ternary operator line occurs after the instruction 'call __main'. Let's highlight that section here:

```
xorl %edx,edx
cmpl $2,(ebp)
setge dl
leal (edx,%edx,4),eax
```

Again, xor is used to set edx to zero. argc is tested against 2 (instead of 1), and dl is set if argc is greater than or equal. If dl gets to 1, the leal instruction directly thereafter will move the value of 5 into eax (because lea (edx,%edx,4) means edx + edx * 4, i.e. edx * 5).
