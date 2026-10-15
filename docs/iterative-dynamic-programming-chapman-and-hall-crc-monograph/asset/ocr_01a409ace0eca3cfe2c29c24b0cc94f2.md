# Appendix A

# Nonlinear algebraic equation solver

Here we include the entire program, written in FORTRAN, to solve a set of nonlinear algebraic equations as entered into the FUN subroutine. The program includes the subroutine RLEQ for the Gaussian elimination.

# A.1  Program listing

```
      IMPLICIT DOUBLE PRECISION (A-H,O-Z)
      DIMENSION A(20,20), ZZ(20), R(20), X(20), F(20), DX(20), DFDX(20,20)
      DIMENSION Z(20), G(20), Y(20), REG(20), XP(20), XS(20), FACT(20)
      DIMENSION GG(20), YY(20), ZB(20)
      OPEN (UNIT=3,FILE='EXAMP106.OUT')
      CALL GETIM(IH,IM,IS,100)
      TMW1 = 1100+100*IS+6000*IM+360000*IH
      N = 2
      NV = 3
      NIT = 25
      X(1) = 0.4D0
      X(2) = 1600.0D0
      WRITE(3,51) (X(I),I=1,N)
   51 FORMAT(1X,'INITIAL VALUES OF X ARE',3F12.5)
      DO 41 IT = 1,NIT
      CALL FUN(X,F,N)
      TEST = 0.0D0
      DO 43 I=1,N
      TEST = TEST + DABS(F(I))
   43 IF(TEST.LT.1.0D-12) GO TO 42
      DO 52 I=1,N
      DX(I) = 1.0D-6*X(I)
      IF(DABS(X(I)).LT.1.0D-6) DX(I) = 1.0D-6
      FACT(I) = 0.5D0/DX(I)
      ZB(I) = X(I)-DX(I)
   52 Z(I) = X(I)+DX(I)
      DO 61 I=1,N
      DO 62 K=1,N
      Y(K) = X(K)
      YY(K) = X(K)
      IF(K.EQ.I) Y(K) = Z(K)
      IF(K.EQ.I) YY(K) = ZB(K)
   62 CONTINUE
      CALL FUN(G,Y,N)
      CALL FUN(GG,YY,N)
      DO 63 J=1,N
      DFDX(J,I) = (G(J)-GG(J))*FACT(I)
   63 CONTINUE
   61 CONTINUE
      DO 31 J=1,N
      R(J) = -F(J)
```