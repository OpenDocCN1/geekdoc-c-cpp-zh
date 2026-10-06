# Optimization Examples

It is up to the reader to compile this new 'optimized' C code, and determine if there is any performance increase. Try compiling this new code without optimizations first, and then compare the new assembly listings to the previous ones.

# 24.5 Example: Instruction Pairings

Q
Why does the dec/jne move operate faster than the equivalent looppnz?

A
The dec/jnz pair operates faster than a loopsz for several reasons. First, dec and jnz pair up in the different modules of the netburst pipeline, so they can be executed simultaneously. With that off the fact that the dec and jnz both require few cycles to execute, while the looppnz (and all the loop instructions, for that matter) instruction takes more cycles to complete. loop instructions are rarely seen out by good compilers.

# 24.6 Example: Avoiding Branches

Below is an assembly version of the expression ? d : 0. There is no branching in the code, how does it work?

```
; ecx = c and eds = d
; eax will contain c ? d : 0 (eax = d if c is not zero, otherwise eax
; = 0)
neg ecx
sbb eax, eax
and eax, edx
ret
```

This is an example of using various arithmetic instructions to avoid branching. The neg instruction sets the carry flag if c is not zero; otherwise, it clears the carry flag. The next line depends on this. If the carry flag is set, sbb results in eax = eax - eax - 1 = 0xffffffff. Otherwise, eax = eax = 0. Finally, performing and on this result ensures that if ecx was not zero in the first place, eax will contain edx, and zero otherwise.

166