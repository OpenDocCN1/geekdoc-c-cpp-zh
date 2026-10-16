As an example, consider the following FORTRAN program:

```
```fortran
REAL TABLE (10), MAXVAL
REAL *, TABLE (1), TABLE (2), TABLE (3)
CALL LRGST (TABLE, 3, MAXVAL)
PRINT *, MAXVAL
END

SUBROUTINE LRGST (A, SIZE, V)
INTEGER SIZE
REAL A (SIZE), V
INTEGER K
V = A (1)
DO 10 K = 1, SIZE
IF (A(K) GT. V) V = A (K)
10 CONTINUE
RETURN
END
```
```

The environment of this program would look as shown in Figure 10.7, where we have added pointers indicating location references that exist immediately after the call to LRGST from the main program.

![](bbox=[0.304, 0.502, 0.731, 0.817])

**Figure 10.7** The runtime environment immediately after a call to the subroutine LRGST