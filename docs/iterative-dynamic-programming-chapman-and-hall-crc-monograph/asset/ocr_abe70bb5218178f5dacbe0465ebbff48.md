```
```fortran
      DO 514 JU=1,NU
514   UR(JU,I) = UR(JU,I)*GAMMA
10    CONTINUE
99    CONTINUE
      CALL GETTIM(IH,IM,IS,1100)
      TIMEF = 1100+100*IS+6000*IM+360000*IH
      TIME = (TIMER-TIMEF)*0.01
      WRITE(3,124) TIME
      WRITE(6,124) TIME
      SHIFT = SHIFT - X(NX) - TF
998   CONTINUE
124   FORMAT(2X,'TIME = ',F17.5,' SECONDS')
      TT = 0.0D0
      DO 275 I=1,NP
      WRITE(4,276) TT, UIN(1,I)
      TT = TT + UIN(2,I)
      WRITE(4,276) TT, UIN(1,I)
275   CONTINUE
276   FORMAT(1X,6F12.5)
      STOP
      END
      SUBROUTINE CSTR(N,T,X,DX)
      IMPLICIT DOUBLE PRECISION(A-H,O-Z)
      DIMENSION X(N), DX(N), U(2)
      COMMON /CONT/ Y,AN,ASTAB
      G3 = 21.87D0*X(4)/(X(4) + 0.4D0) * (X(4) + 62.5D0)
      G2 = X(4)*EXP(-5.0D0*X(4))/(0.1D0 + X(4))
      G1 = 4.75D0*G3/(0.12D0 + G3)
      UP = U(2)*ANP/ASTAB
      FACT = U(1)/X(5)
      DX(1) = UP*(G1*X(2) - X(1)) - FACT*X(1)
      DX(2) = UP*(G2*X(3) - FACT*X(2))
      DX(3) = UP*(G3*X(3) - FACT*X(3))
      DX(4) = UP*(-7.3D0*G3*X(3) + FACT*(20.0D0-X(4)))
      DX(5) = UP*X(1)
      DX(6) = UP
      RETURN
      END
```
```