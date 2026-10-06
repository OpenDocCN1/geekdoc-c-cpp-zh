# Branches

BYTE x;
x = -1;

At the end of this C code, **x** will have the value 1111111: all ones!

When argc is greater than 1, let sets al to zero. Decrementing this value sets every bit in eax to a 1. Now, when we perform the logic **and** function we get:

```
...11111111
&.0000101    ;101 is 5 in binary
----------------
.00000101
```

eax gets the value 5. In this case, it's a roundabout method of doing it, but as a reverser,

For reference, here is the GCC assembly output of the same ternary operator from above:

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

Again, **xor** is used to set edx to zero. argc is tested against 2 (instead of 1), and dl is set if argc is **greater than or equal**. If dl gets to 1, the **leal** instruction directly thereafter will move the value of 5 into eax (because lea (edx,%edx,4) means edx + edx * 4, i.e. edx * 5).