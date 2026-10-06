# Optimization Examples

```
; Line 12
mov eax, esi
cdq
iv ecx
; Line 13
mov esi, ecx
mov ecx, edx
test ecx, ecx
je SHORT $L547
$L563:
; Line 10
mov eax, esi
pop esi
; Line 15
ret 0
_EuclidGCD ENDP
_TEXT ENDS
END
```

At the beginning of the function, eax contains m, and esi contains n. When the instruction "idiv esi" is executed, eax contains the quotient (q), and edx contains the remainder (r). The instruction "mov ecx, edx" moves r into ecx, while q is not used for the rest of the loop, and is therefore discarded.

# 24.4 Example: Decompile Optimized Code

Below is the optimized listing file of the EuclidGCD function, presented in the examples above. Can you decompile this assembly code listing into equivalent 'optimized' C code? How is the optimized version different in structure from the non-optimized version?

```
PUBLIC _EuclidGCD
_TEXT SEGMENT
_m$ = 8 ; size = 4
_n$ = 12 ; size = 4
_EuclidGCD PROC NEAR
; Line 7
mov eax, DWORD PTR _m$[esp-4]
push esi
mov esi, DWORD PTR _n$[esp]
cdq
iv esi
mov ecx, edx
```