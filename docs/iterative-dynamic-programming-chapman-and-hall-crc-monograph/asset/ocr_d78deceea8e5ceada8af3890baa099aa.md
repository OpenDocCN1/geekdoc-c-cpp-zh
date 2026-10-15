```
```fortran
51      CONTINUE
52      CONTINUE
501     CONTINUE
56      FORMAT(1X,I3,F6.3,7F10.6/10X,2F10.6)
        K=NT
        DO 60 I=1,NGX
        TESTP = 1.0D20
        DO 60 L1=1,NRAND
        DO 160 J=1,N
160     X(J) = XG(J,K,I)
        DO 121 J=1,NU
        RAN = URAND(ISEED)
        RN = RAN - 0.5D0
        IF(L1.EQ.1) RN = 0.0D0
        U(J) = UIN(J,K) + RN*UR(J,K)
        UP(J) = U(J)
121     CONTINUE
        T = DBLE(NT-1)
        T = DT*T*AINT
        DO 12 INT=1,NINT
        CALL RUNGK(T,X,N,DT,DX,CSTR)
        T = T + DT
12      CONTINUE
        PERF = X(N)
        IF(PERF.GT.TESTP) GO TO 30
        PERFS = PERF
        DO 122 J=1,NU
        US(J,NT,I) = UP(J)
122     CONTINUE
        TESTP = PERF
30      CONTINUE
60      CONTINUE
        K1 = NT-2
        DO 63 LL=1,K1
        K=NT-LL
        K1=K+1
        DO 61 I=1,NGX
        TESTP = 1.0D20
        DO 64 L1=1,NRAND
        DO 164 J=1,N
164     X(J) = XG(J,K,I)
        T = DBLE(K-1)
        T = DT*T*AINT
        DO 132 J=1,NU
        RAN = URAND(ISEED)
        RN = RAN - 0.5D0
        IF(L1.EQ.1) RN = 0.0D0
        U(J) = UIN(J,K) + RN*UR(J,K)
        UP(J) = U(J)
132     CONTINUE
        DO 13 INT=1,NINT
        CALL RUNGK(T,X,N,DT,DX,CSTR)
        T = T + DT
13      CONTINUE
        DO 33 KK=KL,NT
        IF(NGX.EQ.1) GO TO 502
        TESTD = 3000.0D0
        DO 62 II=1,NGX
        T1 = 0.0D0
        DO 162 JJ=1,N
```
```