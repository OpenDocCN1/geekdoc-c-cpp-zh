At line 16 we compare the value in R2, our inner loop counter, with the limit value in R4. If the value in R2 is greater than or equal to the value in R4, we branch to label PRIME and print the number. We have tried all the alternatives.

```
1  PRIME      SUBENTRY
2             EQUEREGS
3
4             L       R3,'F'3'
5
6  LOOP        A       R3,'F'1'      * CANDIDATE NUMBER TO TEST
7             C       R3,'F'1000'   * DONE?
8             BE      DONE
9
10            LR      R4,R3        * CALCULATE INNER LOOP LIMIT
11            SRA     R4,1         * DIVIDE BY 2
12
13            L       R2,'F'1'      * INNER LOOP COUNTER
14
15 INNER        A       R2,'F'1'
16            CR      R2,R4        * INNER LOOP LIMIT TEST
17            BNL     PRNT
18
19            LR      R6,R3
20            SRDA    R6,32        * PREPARE EVEN/ODD REGISTER PAIR
21            DR      R6,R2
22            C       R6,'F'0'      * CHECK THE REMAINDER
23            BE      LOOP          * NOT PRIME
24            B       INNER
25
26 PRNT         XDECO   R3,OUT
                OUT,L'OUT+L
                'OUT1
28            B       LOOP
29
30 DONE         SUBEXIT
31
32 OUT          DS      CL12
                C' IS
33 OUT1         DC      'PRIME'
34
35            END
```

# Figure 8.8 Search for Prime Numbers

Otherwise, we load the candidate outer loop counter into R6 and double shift it 32 bits to the right into R7. This places the candidate into R7 and (since we are only using positive numbers) zeros out R6. Note: when doing a right arithmetic shift, bits like