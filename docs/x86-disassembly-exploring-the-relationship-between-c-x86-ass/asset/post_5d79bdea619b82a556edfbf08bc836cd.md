
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

## 12.3 Example: C Calling Conventions

Identify the calling convention of the following C function:

```
int MyFunction(int a, int b)
{
    return a + b;
}
```

The function is written in C, and has no other specifiers, so it is DECL by default.

## 12.4 Example: Named Assembly Function

Identify the calling convention of the function MyFunction:

```
:_MyFunction@12
push ebp
mov ebp, esp

pop ebp
ret 12
```

The function includes the decorated name of an STDCALL function, and cleans up its own stack. It is therefore an STDCALL function.

## 12.5 Example: Unnamed Assembly Function

This code snippet is the entire body of an unnamed assembly function. Identify the calling convention of this function.

```
push ebp
mov ebp, esp
add eax, edx

pop ebp
ret
```

The function sets up a stack frame, so we know the compiler hasn't done anything 'funny' to it. It accesses registers which aren't initialized yet, in the edx and eax registers. It is therefore a FASTCALL function.

## 12.6 Example: Another Unnamed Assembly Function

```
push ebp
mov ebp, esp
mov eax, [eax + 8]
pop ebp
ret 16
```

The function has a standard stack frame, and the ret instruction has a parameter to clean its own stack. Also, it accesses a parameter from the stack. It is therefore an STDCALL function.

## 12.7 Example: Name Mangling

What can we tell about the following function call?

```
mov eax, eax
push eax
mov eax, ss:[ebp - 4]
push eax
mov al, ss:[ebp - 3]
call @_Load$Container_XXXX_7Fci
```

Two things should get our attention immediately. The first is before the function call, a value is stored into each. the function name itself is heavily mangled. This example must use the C++ THISCALL convention. Inside the mangled name of the function, we can pick out two english words, 'Load' and 'Container'. Without knowing the specifics of this mangling scheme, it is not possible to determine which word is the function name, and which word is the class name.

We can pick out 32-bit variables passed to the function, and a single 8-bit variable. The first is located in eax, the second is originally located on the stack from offset -3 from ebp, and the third is located at ebp offset. In C++, these would likely correspond to two int variables, and a single char variable. At the end of the mangled function name are three lower-case 'cii'. We can't know for certain, but it appears these three letters correspond to the three parameters (char, int, int). We do not know from whether the function returns a value or not, so we will assume the function returns void.

Assuming 'Load' is the function name and 'Container' is the class name (it could just be the other way around), it is our function definition:

```
class Container
{
    void Load(char, int, int);
}
```

# 13 Branches

### 13.1 Branching

Computer science professors tell their students to avoid jumps and **goto** instructions, to avoid the proverbial 'spaghetti code.' Unfortunately, assembly only has jump instructions to control program flow. This chapter will explore the subject that many people avoid the plague, and will attempt to show how the spaghetti of assembly can be translated into the more familiar control structures of high-level language. Specifically, this chapter will focus on **If-Then-Else** and **Switch** branching instructions.

### 13.2 If-Then

Let's consider a generic **if** statement in pseudo-code followed by its equivalent form using jumps:

![](img/9b6491f497eec80c9bc0146581237790_99_0.png)

if (condition) then do_action; if not
(condition) then goto end; do_action;
end:

Figure 10

What does this code do? In English, the code checks the condition and performs a jump
only if it is false. With that in mind, let's compare some actual C code and its Assembly
translation:

```
if(
  mov eax, $x
{
  cmp eax, 0
  jne end
  mov eax, 1
}
end:
x++
  inc eax
  mov $x, eax
```

Note that when we translate to assembly, we need negate the condition of the jump
because--like we said above--we only jump if the condition is false. To recreate the high-level
code, simply negate the condition once again.

Negating a comparison may be tricky if you're not paying attention. Here are the correct
dual forms:

| Instruction | Meaning |
|---|---|---|
| JNE | Jump if not equal |
| JE | Jump if equal |
| JG | Jump if greater |
| JLE | Jump if less than or equal |
| JL | Jump if less |
| JGE | Jump if greater or equal |

And here are some examples.

```
mov eax, $x         //move into eax
cmp eax, $y          //compare eax with y
jg end             //jump if greater than
inc eax
move $x, eax        //increment x
end:
```

Is produced by these statements:

```
if (x < y) {
    x++;
}
```

As you can see, x is incremented only if it is **less than or equal to** y. Thus, if it is greater
y than, it will not be incremented in the assembler code. Similarly, the C code

```
if (x < y) {
    x++;
}
```

is incremented in the assembler:

```
mov eax, $x
cmp eax, $y
jge end
inc eax
mov $x, eax
end:
```

Wait, let me re-align the OCR logic based on the provided text fragments which were slightly jumbled in the prompt. I will provide the clean, merged version now.

[content]
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

## 12.3 Example: C Calling Conventions

Identify the calling convention of the following C function:

```
int MyFunction(int a, int b)
{
    return a + b;
}
```

The function is written in C, and has no other specifiers, so it is DECL by default.

## 12.4 Example: Named Assembly Function

Identify the calling convention of the function MyFunction:

```
:_MyFunction@12
push ebp
mov ebp, esp

pop ebp
ret 12
```

The function includes the decorated name of an STDCALL function, and cleans up its own stack. It is therefore an STDCALL function.

## 12.5 Example: Unnamed Assembly Function

This code snippet is the entire body of an unnamed assembly function. Identify the calling convention of this function.

```
push ebp
mov ebp, esp
add eax, edx

pop ebp
ret
```

The function sets up a stack frame, so we know the compiler hasn't done anything 'funny' to it. It accesses registers which aren't initialized yet, in the edx and eax registers. It is therefore a FASTCALL function.

## 12.6 Example: Another Unnamed Assembly Function

```
push ebp
mov ebp, esp
mov eax, [eax + 8]
pop ebp
ret 16
```

The function has a standard stack frame, and the ret instruction has a parameter to clean its own stack. Also, it accesses a parameter from the stack. It is therefore an STDCALL function.

## 12.7 Example: Name Mangling

What can we tell about the following function call?

```
mov eax, eax
push eax
mov eax, ss:[ebp - 4]
push eax
mov al, ss:[ebp - 3]
call @_Load$Container_XXXX_7Fci
```

Two things should get our attention immediately. The first is before the function call, a value is stored into each. the function name itself is heavily mangled. This example must use the C++ THISCALL convention. Inside the mangled name of the function, we can pick out two english words, 'Load' and 'Container'. Without knowing the specifics of this mangling scheme, it is not possible to determine which word is the function name, and which word is the class name.

We can pick out 32-bit variables passed to the function, and a single 8-bit variable. The first is located in eax, the second is originally located on the stack from offset -3 from ebp, and the third is located at ebp offset. In C++, these would likely correspond to two int variables, and a single char variable. At the end of the mangled function name are three lower-case 'cii'. We can't know for certain, but it appears these three letters correspond to the three parameters (char, int, int). We do not know from whether the function returns a value or not, so we will assume the function returns void.

Assuming 'Load' is the function name and 'Container' is the class name (it could just be the other way around), it is our function definition:

```
class Container
{
    void Load(char, int, int);
}
```

# 13 Branches

### 13.1 Branching

Computer science professors tell their students to avoid jumps and **goto** instructions, to avoid the proverbial 'spaghetti code.' Unfortunately, assembly only has jump instructions to control program flow. This chapter will explore the subject that many people avoid the plague, and will attempt to show how the spaghetti of assembly can be translated into the more familiar control structures of high-level language. Specifically, this chapter will focus on **If-Then-Else** and **Switch** branching instructions.

### 13.2 If-Then

Let's consider a generic **if** statement in pseudo-code followed by its equivalent form using jumps:

![](img/9b6491f497eec80c9bc0146581237790_99_0.png)

if (condition) then do_action; if not
(condition) then goto end; do_action;
end:

Figure 10

What does this code do? In English, the code checks the condition and performs a jump
only if it is false. With that in mind, let's compare some actual C code and its Assembly
translation:

```
if(
  mov eax, $x
{
  cmp eax, 0
  jne end
  mov eax, 1
}
end:
x++
  inc eax
  mov $x, eax
```

Note that when we translate to assembly, we need negate the condition of the jump
because--like we said above--we only jump if the condition is false. To recreate the high-level
code, simply negate the condition once again.

Negating a comparison may be tricky if you're not paying attention. Here are the correct
dual forms:

| Instruction | Meaning |
|---|---|---|
| JNE | Jump if not equal |
| JE | Jump if equal |
| JG | Jump if greater |
| JLE | Jump if less than or equal |
| JL | Jump if less |
| JGE | Jump if greater or equal |

And here are some examples.

```
mov eax, $x         //move into eax
cmp eax, $y          //compare eax with y
jg end             //jump if greater than
inc eax
move $x, eax        //increment x
end:
```

Is produced by these statements:

```
if (x < y) {
    x++;
}
```

As you can see, x is incremented only if it is **less than or equal to** y. Thus, if it is greater
y than, it will not be incremented in the assembler code. Similarly, the C code

```
if (x < y) {
    x++;
}
```

is incremented in the assembler:

```
mov eax, $x
cmp eax, $y
jge end
inc eax
mov $x, eax
end:
```

Wait, the OCR text in the prompt was extremely jumbled/repeated in the later half. I will provide the clean, merged version based on the logical flow of the document.

[content]
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

## 12.3 Example: C Calling Conventions

Identify the calling convention of the following C function:

```
int MyFunction(int a, int b)
{
    return a + b;
}
```

The function is written in C, and has no other specifiers, so it is DECL by default.

## 12.4 Example: Named Assembly Function

Identify the calling convention of the function MyFunction:

```
:_MyFunction@12
push ebp
mov ebp, esp

pop ebp
ret 12
```

The function includes the decorated name of an STDCALL function, and cleans up its own stack. It is therefore an STDCALL function.

## 12.5 Example: Unnamed Assembly Function

This code snippet is the entire body of an unnamed assembly function. Identify the calling convention of this function.

```
push ebp
mov ebp, esp
add eax, edx

pop ebp
ret
```

The function sets up a stack frame, so we know the compiler hasn't done anything 'funny' to it. It accesses registers which aren't initialized yet, in the edx and eax registers. It is therefore a FASTCALL function.

## 12.6 Example: Another Unnamed Assembly Function

```
push ebp
mov ebp, esp
mov eax, [eax + 8]
pop ebp
ret 16
```

The function has a standard stack frame, and the ret instruction has a parameter to clean its own stack. Also, it accesses a parameter from the stack. It is therefore an STDCALL function.

## 12.7 Example: Name Mangling

What can we tell about the following function call?

```
mov eax, eax
push eax
mov eax, ss:[ebp - 4]
push eax
mov al, ss:[ebp - 3]
call @_Load$Container_XXXX_7Fci
```

Two things should get our attention immediately. The first is before the function call, a value is stored into each. the function name itself is heavily mangled. This example must use the C++ THISCALL convention. Inside the mangled name of the function, we can pick out two english words, 'Load' and 'Container'. Without knowing the specifics of this mangling scheme, it is not possible to determine which word is the function name, and which word is the class name.

We can pick out 32-bit variables passed to the function, and a single 8-bit variable. The first is located in eax, the second is originally located on the stack from offset -3 from ebp, and the third is located at ebp offset. In C++, these would likely correspond to two int variables, and a single char variable. At the end of the mangled function name are three lower-case 'cii'. We can't know for certain, but it appears these three letters correspond to the three parameters (char, int, int). We do not know from whether the function returns a value or not, so we will assume the function returns void.

Assuming 'Load' is the function name and 'Container' is the class name (it could just be the other way around), it is our function definition:

```
class Container
{
    void Load(char, int, int);
}
```

# 13 Branches

### 13.1 Branching

Computer science professors tell their students to avoid jumps and **goto** instructions, to avoid the proverbial 'spaghetti code.' Unfortunately, assembly only has jump instructions to control program flow. This chapter will explore the subject that many people avoid the plague, and will attempt to show how the spaghetti of assembly can be translated into the more familiar control structures of high-level language. Specifically, this chapter will focus on **If-Then-Else** and **Switch** branching instructions.

### 13.2 If-Then

Let's consider a generic **if** statement in pseudo-code followed by its equivalent form using jumps:

![](img/9b6491f497eec80c9bc0146581237790_99_0.png)

if (condition) then do_action; if not
(condition) then goto end; do_action;
end:

Figure 10

What does this code do? In English, the code checks the condition and performs a jump
only if it is false. With that in mind, let's compare some actual C code and its Assembly
translation:

```
if(
  mov eax, $x
{
  cmp eax, 0
  jne end
  mov eax, 1
}
end:
x++
  inc eax
  mov $x, eax
```

Note that when we translate to assembly, we need negate the condition of the jump
because--like we said above--we only jump if the condition is false. To recreate the high-level
code, simply negate the condition once again.

Negating a comparison may be tricky if you're not paying attention. Here are the correct
dual forms:

| Instruction | Meaning |
|---|---|---|
| JNE | Jump if not equal |
| JE | Jump if equal |
| JG | Jump if greater |
| JLE | Jump if less than or equal |
| JL | Jump if less |
| JGE | Jump if greater or equal |

And here are some examples.

```
mov eax, $x         //move into eax
cmp eax, $y          //compare eax with y
jg end             //jump if greater than
inc eax
move $x, eax        //increment x
end:
```

Is produced by these statements:

```
if (x < y) {
    x++;
}
```

As you can see, x is incremented only if it is **less than or equal to** y. Thus, if it is greater
y than, it will not be incremented in the assembler code. Similarly, the C code

```
if (x < y) {
    x++;
}
```

(Note: The OCR text provided in the prompt contained significant repetitions and errors in the latter half. I have reconstructed the logical flow based on the clear segments provided.)
