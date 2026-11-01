
133      BCT      R5,L4      * R5 IS COUNT NBR VALS TO READ
134
135 *    for (i = 0; i < brows * bcols; i++) scanf("%d", b + i);
136
137      SR       R4,R4
138      L        R5,BROWS   * NBR B ROWS
139      M        R4,BCOLS   * TIMES NBR B COLS
140      L        R6,BPTR    * ADDR OF B
141      XREAD    IN,L'IN    * READ LINE
142      LA       R1,IN      * ADDR OF INPUT REC
143 L5    XDECI    R3,0(0,R1) * SCAN INPUT
144      ST       R3,0(0,R6)
145      LA       R6,4(R6)
146      BCT      R5,L5     * R5 IS COUNT NBR VALS TO READ
147
148 *****************************************
149
150 *    printf("Matrix A\n");
151 *    for (i = 0; i < arows; i++) {
152 *        for (j = 0; j < acols; j++) {
153 *            printf("%3d ",*(a + i * acols + j));
154 *        printf("\n");
155 *    }
156 *    printf("\n");
157
158      XPRNT    MSG1,L'MSG1
159
160      L        R3,APTR
161      L        R5,AROWS
162
163 L7    MVI      ROWOUT,C' '
164      MVC      ROWOUT+1(L'ROWOUT-1),ROWOUT
165      L        R6,ACOLS
166      LA       R7,ROWOUT
167
168 L6    MVC      NUM,NUMPAT  * ED PATTERN
169      L        R8,0(0,R3)  * MATRIX VALUE
170      CVD      R8,0       * CVT TO DECIMAL
171      ED       NUM,OUT+6  * CVT TO ZONED
172      MVC      0(4,R7),NUM * ADD TO ROW
173      LA       R7,4(R7)    * ROW PTR
174      LA       R3,4(R3)    * MATRIX PTR
175      BCT      R6,L6      * FOR EACH ROW
176      XPRNT    ROWOUT,L'ROWOUT

264          BL      L10      * NO - ITERATE
265
266          LA      R3,1(0,R3)
267          C       R3,BCOLS    * j < BCOLS
268          BL      L9       * NO - ITERATE
269
270          LA      R2,1(0,R2)
271          C       R2,AROWS    * i < AROWS ?
272          BL      L8       * NO - ITERATE
273
274 ****************************************************************
275
276 *       printf("Matrix C\n");
277 *       for (i = 0; i < arows; i++) {
278 *           for (j = 0; j < bcols; j++) {
279 *               printf("%3d ", *(c + i * bcols + j));
280 *           }
281 *       printf("\n");
282 *       }
283
284          XPRNT   LINE,L'LINE
285
286 *       PRINT RESULT - SAME TECHNIQUE USED ABOVE
287
288          L       R3,CPTR
289          L       R5,CROWS
290
291 L11      MVI     ROWOUT,C' '
292          MVC     ROWOUT+1(L'ROWOUT-1),ROWOUT
293          L       R6,CCOLS
294          LA      R7,ROWOUT
295
296 L12      MVC     NUM,NUMPAT
297          L       R8,0(0,R3)
298          CVD     R8,OUT
299          ED      NUM,OUT+6
300          MVC     0(4,R7),NUM
301          LA      R7,4(0,R7)
302          LA      R3,4(R3)
303          BCT     R6,L12
304          XPRNT   ROWOUT,L'ROWOUT
305          BCT     R5,L11
306
307 *       return 0;

308 *)
    SUBEXIT

311 GADDR   DS    A       * ADDR OF GETMAIN AREA
312 GLEN    DS    F       * AMOUNT GOT
313 IN      DS    CL80
314 OUT     DS    D
315 ROWOUT  DS    CL130
316 MSG1    DC    C'A Matrix'
317 MSG2    DC    C'B Matrix'
318 NUMPAT  DC    X'40202120'
319 NUM     DS    CL4
320 LINE    DC    C'----------------------------------------'
321 TEMP    DS    CL12
         LTORG
         END

Input:
2 3 3 2
1 2 3 4 5 6
7 8 9 10 11 12

Output:
A Matrix
  1  2  3
  4  5  6
B Matrix
  7  8
  9 10
 11 12
----------------------------------------
 58  64
139 154

## Figure 98 Matrix Multiplication

## 24. General Instruction Set

Note: The letter C in the format column means that the instruction sets the Condition Code.

| Instruction | Mnemonic | Format | OpCode |
|---|---|---|---|
| ADD (extended BFP) | AXBR | RRE C | B34A |
| ADD (long BFP) | ADGR | RRE C | B31A |
| ADD (long BFP) | ADB | RXE C | E01A |
| ADD (short BFP) | AESR | RRE C | B30A |
| ADD (short BFP) | AEB | RXE C | E00A |
| ADD (32) | AR | RR C | 1A |
| ADD (32) | A | RX C | 5A |
| ADD (32) | AY | RXY C | E35A |
| ADD (64<32) | AGFR | RRE C | B918 |
| ADD (64<32) | AGF | RXY C | E318 |
| ADD (64) | AGR | RRE C | B908 |
| ADD (64) | AG | RXY C | E308 |
| ADD DECIMAL | AP | SS C | FA |
| ADD HALFWORD | AH | RX C | 4A |
| ADD HALFWORD | ARY | RXY C | E27A |
| ADD HALFWORD IMMEDIATE (32) | AHI | RI C | A7A |
| ADD HALFWORD IMMEDIATE (64) | AGHI | RI C | A7B |
| ADD LOGICAL (32) | ALR | RR C | 1E |
| ADD LOGICAL (32) | AL | RX C | 5E |
| ADD LOGICAL (32) | ALY | RXY C | E35E |
| ADD LOGICAL (64<32) | ALGFR | RRE C | B91A |
| ADD LOGICAL (64<32) | ALGF | RXY C | E31A |
| ADD LOGICAL (64) | ALGR | RRE C | B90A |
| ADD LOGICAL (64) | ALG | RXY C | E30A |
| ADD LOGICAL WITH CARRY (32) | ALCR | RRE C | B998 |
| ADD LOGICAL WITH CARRY (32) | ALC | RXY C | E398 |
| ADD LOGICAL WITH CARRY (64) | ALCGR | RRE C | B968 |
| ADD LOGICAL WITH CARRY (64) | ALCG | RXY C | E368 |
| ADD NORMALIZED (extended HFP) | AXR | RR C | 36 |
| ADD NORMALIZED (long HFP) | ADR | RR C | 2A |
| ADD NORMALIZED (long HFP) | AD | RX C | 6A |
| ADD NORMALIZED (short HFP) | ANR | RR C | 3A |
| ADD NORMALIZED (short HFP) | AE | RX C | 7A |
| ADD UNNORMALIZED (long HFP) | AWR | RR C | 2E |
| ADD UNNORMALIZED (long HFP) | AM | RX C | 6E |
| ADD UNNORMALIZED (short HFP) | AUR | RR C | 3E |
| ADD UNNORMALIZED (short HFP) | AU | RX C | 7E |
| AND (character) | NC | SS C | D4 |
| AND (immediate) | WI | SI C | 94 |
| AND (immediate) | WITY | SIY C | E354 |
| AND (32) | NR | RR C | 14 |
| AND (32) | N | RX C | 54 |
| AND (32) | NY | RXY C | B254 |
| AND (64) | NGR | RRE C | B998 |
| AND (64) | NG | RXY C | B380 |
| AND IMMEDIATE (high high) | NIHH | RI C | A54 |
| AND IMMEDIATE (high low) | NIHL | RI C | A55 |
| AND IMMEDIATE (low high) | NILH | RI C | A56 |
| AND IMMEDIATE (low low) | NILL | RI C | A57 |
| BRANCH AND LINK | BALR | RR | 05 |
| BRANCH AND LINK | BAL | RX | 45 |
| BRANCH AND SAVE | BASR | RR | 0D |
| BRANCH AND SAVE | BAS | RX | 4D |
| BRANCH AND SAVE AND SET MODE | BASSM | RR | 0C |
| BRANCH AND SET AUTHORITY | BSA | RRE | B25A |
| BRANCH AND SET MODE | BSM | RR | 0B |
| BRANCH AND STACK | BAKR | RRE | B240 |
| BRANCH IN SUBSPACE GROUP | BSG | RRE | B258 |
| BRANCH ON CONDITION | BCR | RX | 07 |
| BRANCH ON CONDITION | BC | RX | 47 |
| BRANCH ON COUNT (32) | BCTR | RR | 06 |
| BRANCH ON COUNT (32) | BCT | RX | 46 |
| BRANCH ON COUNT (64) | BCTGR | RRE | B946 |
| BRANCH ON COUNT (64) | BCTG | RXY | B346 |
| BRANCH ON INDEX HIGH (32) | BXH | RS | B6 |
| BRANCH ON INDEX HIGH (64) | BXHG | RSY | B844 |
| BRANCH ON INDEX LOW OR EQUAL (32) | BXLE | RS | B7 |
| BRANCH ON INDEX LOW OR EQUAL (64) | BXLEG | RSY | B845 |
| BRANCH RELATIVE AND SAVE | BRAS | RI | A75 |
| BRANCH RELATIVE AND SAVE LONG | BRASL | RIL | C05 |
| BRANCH RELATIVE ON CONDITION | BRC | RI | A74 |
| BRANCH RELATIVE ON CONDITION LONG | BRCL | RIL | C04 |
| BRANCH RELATIVE ON COUNT (32) | BRCT | RI | A76 |
| BRANCH RELATIVE ON COUNT (64) | BRCTG | RI | A77 |
| BRANCH RELATIVE ON INDEX HIGH (32) | BRXH | RSI | B4 |
| BRANCH RELATIVE ON INDEX HIGH (64) | BRXHG | RIE | EC44 |
| BRANCH RELATIVE ON INDEX L OR E (32) | BRXLE | RSI | B5 |
| BRANCH RELATIVE ON INDEX L OR E (64) | BRXLG | RIE | EC45 |
| CANCEL SUBCHANNEL | XSCH | S C | B276 |
| CHECKSUM | CKSM | RRE C | B241 |
| CIPHER MESSAGE | KM | RRE C | B92E |
| CIPHER MESSAGE WITH CHAINING | KMC | RRE C | B92F |
| CLEAR SUBCHANNEL | CSCH | S C | B230 |
| COMPARE (extended BFP) | CXBR | RRE C | B349 |
| COMPARE (extended HFP) | CXR | RRE C | B369 |
| COMPARE (long BFP) | CDBR | RRE C | B319 |
| COMPARE LOGICAL C. UNDER MASK (low) | CLMY | RSY C | E821 |
| COMPARE LOGICAL LONG | CLCL | RR C | 09 |
| COMPARE LOGICAL LONG EXTENDED | CLCLE | RS C | A3 |
| COMPARE LOGICAL LONG UNICODE | CLCLU | RSY C | EBBF |
| COMPARE LOGICAL STRING | CLST | RRE C | B25D |
| COMPARE UNTIL SUBSTRING EQUAL | CUSE | RRE C | B257 |
| COMPRESSION CALL | CMPBC | RRE C | B263 |
| COMPUTE INTERMEDIATE MESSAGE DIGEST | KIMD | RRE C | B91E |
| COMPUTE LAST MESSAGE DIGEST | KLMD | RRE C | B93F |
| COMPUTE MESSAGE AUTHENTICATION CODE | KMAC | RRE C | B91F |
| CONVERT BFP TO HFP (long) | THDR | RRE C | B359 |
| CONVERT BFP TO HFP (short to long) | THEDR | RRE C | B358 |
| CONVERT FROM FIXED (32 to ext. BFP) | CXFBR | RRE | B396 |
| CONVERT FROM FIXED (32 to ext. HFP) | CXFR | RRE | B3B6 |
| CONVERT FROM FIXED (32 to long BFP) | CDFBR | RRE | B395 |
| CONVERT FROM FIXED (32 to long HFP) | CDFR | RRE | B385 |
| CONVERT FROM FIXED (32 to short BFP) | CEFBR | RRE | B394 |
| CONVERT FROM FIXED (32 to short HFP) | CEFR | RRE | B384 |
| CONVERT FROM FIXED (64 to ext. BFP) | CXGBR | RRE | B3A6 |
| CONVERT FROM FIXED (64 to ext. HFP) | CXG8R | RRE | B3C6 |
| CONVERT FROM FIXED (64 to long BFP) | CDG8R | RRE | B3A5 |
| CONVERT FROM FIXED (64 to long HFP) | CDG8R | RRE | B3C5 |
| CONVERT FROM FIXED (64 to short BFP) | CEG8R | RRE | B3A4 |
| CONVERT FROM FIXED (64 to short HFP) | CEG8R | RRE | B3C4 |
| CONVERT HFP TO BFP (long to short) | TBEDR | RRF C | B350 |
| CONVERT HFP TO BFP (long) | TBDR | RRF C | B351 |
| CONVERT TO BINARY (32) | CVB | RX | 4F1 |
| CONVERT TO BINARY (32) | CVBY | RXY | B306 |
| CONVERT TO BINARY (64) | CVBG | RRF | B30E |
| CONVERT TO DECIMAL (32) | CVD | RX | 4E |
| CONVERT TO DECIMAL (32) | CVDY | RXY | B226 |
| CONVERT TO DECIMAL (64) | CVDG | RXY | B2E8 |
| CONVERT TO FIXED (ext. BFP to 32) | CXFGBR | RRF C | B3A9 |
| CONVERT TO FIXED (ext. BFP to 64) | CXG8BR | RRF C | B3AA |
| CONVERT TO FIXED (ext. HFP to 32) | CXFR | RRF C | B3BA |
| CONVERT TO FIXED (ext. HFP to 64) | CXGR | RRF C | B3CA |
| CONVERT TO FIXED (long BFP to 32) | CDFBR | RRF C | B3B9 |
| CONVERT TO FIXED (long BFP to 64) | CDG8BR | RRF C | B3A9 |
| CONVERT TO FIXED (long HFP to 32) | CDFR | RRF C | B3B9 |
| CONVERT TO FIXED (long HFP to 64) | CDG8R | RRF C | B3C9 |
| CONVERT TO FIXED (short BFP to 32) | CEFBR | RRF C | B3B9 |
| CONVERT TO FIXED (short BFP to 64) | CEG8BR | RRF C | B3A8 |
| CONVERT TO FIXED (short HFP to 32) | CEFR | RRF C | B3B8 |
| CONVERT TO FIXED (short HFP to 64) | CEG8R | RRF C | B3C8 |
| CONVERT UNICODE TO UTF-8 | CUUTF | RRE C | B2A6 |
