There are several obvious advantages to the DSECT approach not the least of which are readability. It should also be noted that, should the data structure change, say, to enlarge the name field, it need be done only in the DSECT itself and not in each of the XPRNT statements.

```
1  ID      DSECT
2  NAME    DS      CL30
3  CITY    DS      CL30
4  STATE   DS      CL2
5  ZIP     DS      CL5
6  PHONE   DS      CL10
7  PGM     CSECT
8         LA      R2,ARRAY
9         USING   ID,R2
10        L       R3,=F'1000'
11 LOOP    XPRNT   NAME,L'NAME      * NAME
12        XPRNT   CITY,L'CITY      * CITY
13        XPRNT   STATE,L'STATE    * STATE
14        XPRNT   ZIP,L'ZIP        * ZIP
15        XPRNT   PHONE,L'PHONE    * PHONE
16        LA      R2,77(0,R2)      * INCR POINTER
17        BCT     R3,LOOP
```

Figure 65 Table with DSECT