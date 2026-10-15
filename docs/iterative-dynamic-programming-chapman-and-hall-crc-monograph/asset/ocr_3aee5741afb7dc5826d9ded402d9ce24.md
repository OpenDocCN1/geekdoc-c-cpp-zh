# Appendix B

# Listing of linear programming program

Here we include the entire program, written in FORTRAN, to accomplish the 5 food diet problem with linear programming. The program, written in single precision, is divided into the main program and 3 subroutines. This computer program is the only one used in this book that is written in single precision.

# B.1 Main program for the diet problem

```
DIMENSION A(10,20),B(10),C(20),CC(20),Z(21),ZZ(21)
DIMENSION TITLE(20),FOOD(7,5)
COMMON CC,ZZ,Z,FOOD
CALL GETTIM(IH,IM,IS,I100)
STTIME = I100 + 100*IS + 6000*IM + 360000*IH
CALL INPUT(A,N,M,B,C,M1,TITLE)
CALL SIMP(A,N,M,B,C,M1)
CALL OUTPUT(A,N,M,B,C,M1,TITLE)
CALL GETTIM(IH,IM,IS,I100)
ENDTIME = I100 + 100*IS + 6000*IM + 360000*IH
TIME = (ENDTIME-STTIME)*0.01
WRITE(6,197) TIME
WRITE(3,197) TIME
197 FORMAT(5X,'CPU TIME =',F12.5,' SECONDS')
STOP
END
```