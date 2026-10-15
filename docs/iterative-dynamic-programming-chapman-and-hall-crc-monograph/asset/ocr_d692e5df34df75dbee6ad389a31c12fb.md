```
```fortran
      DO 100 IT = 1,NIT
      DO 94 J=1,NR
      DO 52 I=1,N
      RN = URAND(ISEED)
      RAN = 2.00D*(RN - 0.5)
      IF(J.EQ.1) RAN = 0.0
      X(I) = XP(I) + RAN*REG(I)
      IF(X(I).LT.0.0D0) X(I) = 0.0D0
      IF(X(I).GT.BETA(I)) X(I) = BETA(I)
   52 CONTINUE
      T1 = 1.25D0*X(1)+0.90D0*X(2)+0.99D0*X(3)+1.1D0*X(4)+0.79D0*X(5)
      IF(T1.GT.4.0D0) GO TO 30
      T2 = 1.5D2*X(1)+2.0D2*X(2)+2.45D2*X(3)+2.7D2*X(4)+9.0D1*X(5)
      IF(T2.GT.8.0D2) GO TO 30
      T3 = X(1)+7.0D0*X(2)+2.1D1*X(3)+8.6D0*X(4)+2.0D0*X(5)
      IF(T3.LT.25.0D0) GO TO 30
      T4 = 0.7D0*X(2)+2.7D0*X(3)+1.3D0*X(4)+X(5)
      IF(T4.LT.3.5D0) GO TO 30
      P = 1.0D2*X(1)+5.0D1*X(2)+2.5D1*X(3)+2.0D1*X(4)+3.5D1*X(5)
      IF(P.LT.TEST) GO TO 30
      NO = NO + 1
      TEST = P
      DO 43 I=1,N
   43 XS(I) = X(I)
   30 CONTINUE
   94 CONTINUE
      IF(LW.LT.LIM) GO TO 51
      WRITE(3,73) IT,NO,XS(I),I=1,N),TEST
   73 FORMAT(1X,2I7,5F12.7/10X,3F12.7)
      LW=0
   51 LW = LW+1
  171 FORMAT(1X,5F13.7)
  172 FORMAT(1X,'PASS NUMBER =', I5, ' P = ',D16.7)
      DO 95 I=1,N
      REG(I) = REG(I)*RED
      XP(I) = XS(I)
   95 CONTINUE
  100 CONTINUE
      WRITE(6,171) (XS(I),I=1,N)
      WRITE(3,171) (XS(I),I=1,N)
      WRITE(6,172) IPASS,TEST
      WRITE(3,172) IPASS,TEST
      CALL GETTIM(IH,IM,IS,1100)
      ENDTIME = 1100 + 100*IS + 6000*IM + 360000*IH
      TIME = (ENDTIME-STTIME)*0.01
      WRITE(6,197) TIME
      WRITE(3,197) TIME
      DO 202 I=1,N
      REG(I) = DABS(Y$(I) - XS(I))
      IF(REG(I).LT.EPS) REG(I) = EPS
      Y$(I) = XS(I)
  202 CONTINUE
  200 CONTINUE
  197 FORMAT(5X,'CPU TIME =',F12.5,' SECONDS')
      STOP
      END
```
```