# 24 Optimization Examples

# 24.1 Example: Optimized vs Non-Optimized Code

The following example is adapted from an algorithm presented in Knuth(vol 1, chap 1) used to find the greatest common denominator of 2 integers. Compare the listing file of this function when compiler optimizations are turned on and off.

```
/line i=/
int EuclidGCD(int m
```

Compiling with the Microsoft C compiler, we generate a listing file using no optimization:

```
PUBLIC _EuclidsGCD
_TEXT SEGMENT
_r = -8; size = 4
_q = -4; size = 4
_m = 12; size = 4
_EuclidGCD PROC NEAR
: Line 2
push ebp
mov ebp, esp
sub ebp, 8
$L477:
```