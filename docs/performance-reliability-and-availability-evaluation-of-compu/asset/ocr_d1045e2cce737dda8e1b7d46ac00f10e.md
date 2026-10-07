# 686 Performance, Reliability, and Availability Evaluation of Computational Systems

```
IILOOP:
N1 = 0;
N2 = 12 * LOOP;
N3 = 14 * LOOP;
N4 = 345 * LOOP;
N6 = 210 * LOOP;
N7 = 32 * LOOP;
N8 = 899 * LOOP;
N9 = 616 * LOOP;
N10 = 0;
N11 = 93 * LOOP;
```

```
/*
C Module 1: Simple identifiers
C
/*
X1 = 1.0;
X2 = -1.0;
X3 = -1.0;
X4 = -1.0;
```

```
for (I = 1; I <= N1; I++) {
nX1 = (X1 + X2 - X3 + X4) * T;
X2 = (X1 + X2 - X3 + X4) * T;
X3 = (X1 - X2 + X3 + X4) * T;
X4 = (-X1 + X2 + X3 + X4) * T;
}
#ifndef PRINTOUT
IF (JJ==II) POUT(N1,N1,N1,X1,X2,X3,X4);
#endif
```

```
/*
C Module 2: Array elements
C
/*
El[1] = 1.0;
El[2] = -1.0;
El[3] = -1.0;
El[4] = -1.0;
```

```
for (I = 1; I <= N2; I++) {
E[1] = (E[1] + E[2] + E[3] - E[4]) * T;
E[2] = (E[1] + E[2] - E[3] + E[4]) * T;
E[3] = (E[1] - E[2] + E[3] + E[4]) * T;
E[4] = (-E[1] + E[2] + E[3] + E[4]) * T;
}
#ifndef PRINTOUT
IF (JJ==II) POUT(N2,N3,N2,E[1],E[2],E[3],E[4]);
#endif
```