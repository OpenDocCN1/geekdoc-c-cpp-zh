
# Float to Int Conversions

```
.long 1073741824
.align 8 0
LC1:
.long 1074266112
.global def @MyFunction320:
.cli 2; .type 32; .endef
@MyFunction320:
    ebp
    pushl
    mov %esp, %ebp
    sub $16, %esp
    fld 8(%ebp)
    fstpl -8(%ebp)
    fld 16(%ebp)
    fstpl -16(%ebp)
    fld -8(%ebp)
    faddp %xst, %x1
    fld -16(%ebp)
    LC0:
    faddp %xst, %x1
fmul
    fld 24(%ebp)
LC10:
    faddp %xst, %x1
fmul
    faddp %xst, %x1
leave
ret $20
```

Here we can also see, after all the opening nonsense, that [eb - 8] (originally [eb + 8]) is value x, and that [eb - 24] (originally [eb - 24]) is value z. These parameters are therefore passed right-to-left. Also, we can deduce from the final fmul instruction that the result is passed in ST0. Again, the STDCALL function cleans its own stack, as we would expect.

## 21.2.4 Conclusions

Floating point values are passed as parameters on the stack, and are passed on the FPU stack as results. Floating point values do not get put into the general-purpose integer registers (eax, ebx, ebx, etc.), so STDCALL functions that only have floating point parameters collapse into STDCALL instead. **double** values are 8-bytes wide, and therefore will take up 8-bytes on the stack. **float** values however, are only 4-bytes wide.

## 21.3 Float to Int Conversions

## 21.4 FPU Compares and Jumps

## 22 Floating Point Examples

### 22.1 Example: Floating Point Arithmetic

Here is the C source code, the GCC assembly listing of a simple C language function that performs simple floating-point arithmetic. Can you determine what the numerical values of LC5 and LC6 are?

```
__fastcall double MyFunction(double x, double y, float z)
{
  return (x + 1.0) * (y + 2.0) * (z + 3.0);
}
```

```
.align 8
LC5:
.long 0
.long 1073741824
.align 8
LC6:
.long 0
.long 1074266112
.globl @MyFunction2@0
.def @MyFunction2@0; .scl 2; .type 32; .ndef
@MyFunction2@:
push %Xeb
movl x,%Xeb
sub $16,%Xeb
fdl 8(%Xeb)
lfstp -8(%Xeb)
fdl 16(%Xeb)
lfstp -16(%Xeb)
fdl
fadd %Xst,%Xst(1)
fdl -16(%Xeb)
fdl
LCS
faddp %Xst,%Xst(1)
mul %Xst,%Xst(1)
```

```
flds 24(%ebp)
fld1 LC6
fadd %xst, %st(i)
mul %xst, %st(i)
leave
ret $20
```

For this, we don't even need a floating-point number calculator, although you are free to use one if you wish (and if you can find a good one). LC5 is added to [ebp - 16], which we know to be y, and LC6 is added to [ebp - 24], which we know to be z. Therefore, LC5 is the number "2.0", and LC6 is the number "3.0". Notice that the fld1 instruction automatically loads the top of the floating-point stack with the constant value "1.0".

## 23 Code Optimization

### 23.1 Code Optimization

An optimizing compiler is perhaps one of the most complicated, powerful, and most interesting programs in existence. This chapter will talk about optimizations, although this chapter will not include a table of common optimizations.

### 23.2 Stages of Optimizations

There are two times when a compiler can perform optimizations: first, in the intermediate representation, and second, during the code generation.

### 23.2.1 Intermediate Representation Optimizations

While in the intermediate representation, a compiler can perform various optimizations, often based on dataflow analysis techniques. For example, consider the following code fragment:

```
x = 5;
if(x != 5)
{
  //loop body
}
```

An optimizing compiler might notice that at the point of 'if (x != 5)', the value of x is always the constant '5'. This allows substituting '5' for x resulting in '5 != 5'. Then the compiler notices that the resulting expression operates entirely on constants, so the value can be calculated instead of at run time, optimizing the conditional to 'if (false)'. Finally the compiler sees that the body of the if will never be executed, so it can omit the entire body of the if conditional altogether.

Consider the reverse case:

```
x = 5;
if(x == 5)
{
  //loop body
}
```

In this case, the optimizing compiler would notice that the IF conditional will always be true, and it won't even bother writing code to test x.

### 23.2.2 Control Flow Optimizations

Another set of optimization which can be performed either at the intermediate or the code generation level are control flow optimizations. Most of these optimizations deal with the elimination of useless branches. Consider the following code:

```
if (A)
{
    if (B)
    {
        C;
    } else
{
        D;
    }
} else
{
    E;
}
end_A;
```

In this code, a simplistic compiler would generate a jump from the C block to end_B, and then another jump from end_B to end_A (to get the E statements). Clearly jumping to a jump is inefficient, so optimizing compilers will generate a direct jump from block C to end_A.

This unfortunately will make the code more confused and will prevent a nice recovery of the original code. For complex functions, it's possible that one will have to consider the code made of only if()-goto; sequences, without being able to identify higher level statements like if-else or loops.

The process of identifying high level statement hierarchies is called 'code structuring'.

### 23.2.3 Code Generation Optimizations

Once the compiler has sifted through all the logical inefficiencies in your code, the code generator takes over. Often the code generator will replace certain slow machine instructions with faster machine instructions.

For instance, the instruction:

```
beginning:
...
loopnz beginning
```

operates much slower than the equivalent instruction set:

```
beginning:
...
dec ecz
jne beginning
```

147

So then would a compiler ever use a loopxx instruction? The answer is that most optimizing compilers never use loopxx, and therefore as a it makes more sense to use the following instruction:

```
mov eax, 0
```

What about the instruction:

```
xor eax
```

147

```
mov eax,0
```
