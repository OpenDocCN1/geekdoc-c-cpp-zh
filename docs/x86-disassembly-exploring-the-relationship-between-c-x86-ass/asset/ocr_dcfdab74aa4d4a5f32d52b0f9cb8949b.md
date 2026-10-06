# Calling Convention Examples

```
.global _MyFunction@24
    _MyFunction@24: .scl 2; .type 32; .endef
_MyFunction@24:
    push %ebp
    mov %ebp, %eax
    movl 8(%ebp), %eax
    imull 12(%ebp), %edx
    movl 16(%ebp), %edx
    movl %edx, %eax
    incl %eax
    imull
    movl 20(%ebp), %edx
    addl $2, %edx
    movl 24(%ebp), %edx
    addl $3, %edx
    imull
    movl 28(%ebp), %edx
    movl %edx, %eax
    pop %ebp
    ret $24
```

We can see here that values at +8 and +12 from a are still x and y, respectively. The value at +16 is incremented by 1, the value at +20 is incremented by 2, etc all the way to the value at +28. We can then create the following table:

| x = [ebp - 8] |
| y = [ebp - 12] |
| a = [ebp - 16] |
| b = [ebp - 20] |
| c = [ebp - 24] |
| d = [ebp - 28] |

With c being pushed first, and x being pushed last. Therefore, these parameters are also pushed in right-to-left order. This function then cleans 24 bytes off the stack with the 'ret 24' instruction.

# 12.3 Example: C Calling Conventions

Identify the calling convention of the following C function:

```
int MyFunction(int a, int b)
{
    return a + b;
}
```

The function is written in C, and has no other specifiers, so it is DECL by default.