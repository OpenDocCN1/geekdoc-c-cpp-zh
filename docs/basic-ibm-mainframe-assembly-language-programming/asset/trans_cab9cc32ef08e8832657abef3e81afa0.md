
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

输入：
2 3 3 2
1 2 3 4 5 6
7 8 9 10 11 12

输出：
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

## 图98 矩阵乘法

## 24. 通用指令集

注意：格式列中的字母 C 表示该指令会设置条件码。

| 指令 | 助记符 | 格式 | 操作码 |
|---|---|---|---|
| 加法（扩展BFP） | AXBR | RRE C | B34A |
| 加法（长BFP） | ADGR | RRE C | B31A |
| 加法（长BFP） | ADB | RXE C | E01A |
| 加法（短BFP） | AESR | RRE C | B30A |
| 加法（短BFP） | AEB | RXE C | E00A |
| 加法（32） | AR | RR C | 1A |
| 加法（32） | A | RX C | 5A |
| 加法（32） | AY | RXY C | E35A |
| 加法（64<32） | AGFR | RRE C | B918 |
| 加法（64<32） | AGF | RXY C | E318 |
| 加法（64） | AGR | RRE C | B908 |
| 加法（64） | AG | RXY C | E308 |
| 十进制加法 | AP | SS C | FA |
| 半字加法 | AH | RX C | 4A |
| 半字加法 | ARY | RXY C | E27A |
| 半字立即数加法（32） | AHI | RI C | A7A |
| 半字立即数加法（64） | AGHI | RI C | A7B |
| 逻辑加法（32） | ALR | RR C | 1E |
| 逻辑加法（32） | AL | RX C | 5E |
| 逻辑加法（32） | ALY | RXY C | E35E |
| 逻辑加法（64<32） | ALGFR | RRE C | B91A |
| 逻辑加法（64<32） | ALGF | RXY C | E31A |
| 逻辑加法（64） | ALGR | RRE C | B90A |
| 逻辑加法（64） | ALG | RXY C | E30A |
| 带进位逻辑加法（32） | ALCR | RRE C | B998 |
| 带进位逻辑加法（32） | ALC | RXY C | E398 |
| 带进位逻辑加法（64） | ALCGR | RRE C | B968 |
| 带进位逻辑加法（64） | ALCG | RXY C | E368 |
| 规格化加法（扩展HFP） | AXR | RR C | 36 |
| 规格化加法（长HFP） | ADR | RR C | 2A |
| 规格化加法（长HFP） | AD | RX C | 6A |
| 规格化加法（短HFP） | ANR | RR C | 3A |
| 规格化加法（短HFP） | AE | RX C | 7A |
| 非规格化加法（长HFP） | AWR | RR C | 2E |
| 非规格化加法（长HFP） | AM | RX C | 6E |
| 非规格化加法（短HFP） | AUR | RR C | 3E |
| 非规格化加法（短HFP） | AU | RX C | 7E |
| 逻辑与（字符） | NC | SS C | D4 |
| 逻辑与（立即数） | WI | SI C | 94 |
| 逻辑与（立即数） | WITY | SIY C | E354 |
| 逻辑与（32） | NR | RR C | 14 |
| 逻辑与（32） | N | RX C | 54 |
| 逻辑与（32） | NY | RXY C | B254 |
| 逻辑与（64） | NGR | RRE C | B998 |
| 逻辑与（64） | NG | RXY C | B380 |
| 立即数逻辑与（高-高） | NIHH | RI C | A54 |
| 立即数逻辑与（高-低） | NIHL | RI C | A55 |
| 立即数逻辑与（低-高） | NILH | RI C | A56 |
| 立即数逻辑与（低-低） | NILL | RI C | A57 |
| 分支并链接 | BALR | RR | 05 |
| 分支并链接 | BAL | RX | 45 |
| 分支并保存 | BASR | RR | 0D |
| 分支并保存 | BAS | RX | 4D |
| 分支、保存并设置模式 | BASSM | RR | 0C |
| 分支并设置权限 | BSA | RRE | B25A |
| 分支并设置模式 | BSM | RR | 0B |
| 分支并压栈 | BAKR | RRE | B240 |
| 子空间组内分支 | BSG | RRE | B258 |
| 按条件分支 | BCR | RX | 07 |
| 按条件分支 | BC | RX | 47 |
| 按计数分支（32） | BCTR | RR | 06 |
| 按计数分支（32） | BCT | RX | 46 |
| 按计数分支（64） | BCTGR | RRE | B946 |
| 按计数分支（64） | BCTG | RXY | B346 |
| 按索引高分支（32） | BXH | RS | B6 |
| 按索引高分支（64） | BXHG | RSY | B844 |
| 按索引低或等于分支（32） | BXLE | RS | B7 |
| 按索引低或等于分支（64） | BXLEG | RSY | B845 |
| 相对分支并保存 | BRAS | RI | A75 |
| 长相对分支并保存 | BRASL | RIL | C05 |
| 按条件相对分支 | BRC | RI | A74 |
| 按条件长相对分支 | BRCL | RIL | C04 |
| 按计数相对分支（32） | BRCT | RI | A76 |
| 按计数相对分支（64） | BRCTG | RI | A77 |
| 按索引高相对分支（32） | BRXH | RSI | B4 |
| 按索引高相对分支（64） | BRXHG | RIE | EC44 |
| 按索引低或等于相对分支（32） | BRXLE | RSI | B5 |
| 按索引低或等于相对分支（64） | BRXLG | RIE | EC45 |
| 取消子通道 | XSCH | S C | B276 |
| 校验和 | CKSM | RRE C | B241 |
| 加密消息 | KM | RRE C | B92E |
| 带链接的加密消息 | KMC | RRE C | B92F |
| 清除子通道 | CSCH | S C | B230 |
| 比较（扩展BFP） | CXBR | RRE C | B349 |
| 比较（扩展HFP） | CXR | RRE C | B369 |
| 比较（长BFP） | CDBR | RRE C | B319 |
| 按掩码逻辑字符比较（低位） | CLMY | RSY C | E821 |
| 长逻辑比较 | CLCL | RR C | 09 |
| 扩展长逻辑比较 | CLCLE | RS C | A3 |
| Unicode长逻辑比较 | CLCLU | RSY C | EBBF |
| 字符串逻辑比较 | CLST | RRE C | B25D |
| 比较直到子串相等 | CUSE | RRE C | B257 |
| 压缩调用 | CMPBC | RRE C | B263 |
| 计算中间消息摘要 | KIMD | RRE C | B91E |
| 计算最终消息摘要 | KLMD | RRE C | B93F |
| 计算消息认证码 | KMAC | RRE C | B91F |
| 将BFP转换为HFP（长） | THDR | RRE C | B359 |
| 将BFP转换为HFP（短到长） | THEDR | RRE C | B358 |
| 从定点转换（32位到扩展BFP） | CXFBR | RRE | B396 |
| 从定点转换（32位到扩展HFP） | CXFR | RRE | B3B6 |
| 从定点转换（32位到长BFP） | CDFBR | RRE | B395 |
| 从定点转换（32位到长HFP） | CDFR | RRE | B385 |
| 从定点转换（32位到短BFP） | CEFBR | RRE | B394 |
| 从定点转换（32位到短HFP） | CEFR | RRE | B384 |
| 从定点转换（64位到扩展BFP） | CXGBR | RRE | B3A6 |
| 从定点转换（64位到扩展HFP） | CXG8R | RRE | B3C6 |
| 从定点转换（64位到长BFP） | CDG8R | RRE | B3A5 |
| 从定点转换（64位到长HFP） | CDG8R | RRE | B3C5 |
| 从定点转换（64位到短BFP） | CEG8R | RRE | B3A4 |
| 从定点转换（64位到短HFP） | CEG8R | RRE | B3C4 |
| 将HFP转换为BFP（长到短） | TBEDR | RRF C | B350 |
| 将HFP转换为BFP（长） | TBDR | RRF C | B351 |
| 转换为二进制（32） | CVB | RX | 4F1 |
| 转换为二进制（32） | CVBY | RXY | B306 |
| 转换为二进制（64） | CVBG | RRF | B30E |
| 转换为十进制（32） | CVD | RX | 4E |
| 转换为十进制（32） | CVDY | RXY | B226 |
| 转换为十进制（64） | CVDG | RXY | B2E8 |
| 转换为定点（扩展BFP到32位） | CXFGBR | RRF C | B3A9 |
| 转换为定点（扩展BFP到64位） | CXG8BR | RRF C | B3AA |
| 转换为定点（扩展HFP到32位） | CXFR | RRF C | B3BA |
| 转换为定点（扩展HFP到64位） | CXGR | RRF C | B3CA |
| 转换为定点（长BFP到32位） | CDFBR | RRF C | B3B9 |
| 转换为定点（长BFP到64位） | CDG8BR | RRF C | B3A9 |
| 转换为定点（长HFP到32位） | CDFR | RRF C | B3B9 |
| 转换为定点（长HFP到64位） | CDG8R | RRF C | B3C9 |
| 转换为定点（短BFP到32位） | CEFBR | RRF C | B3B9 |
| 转换为定点（短BFP到64位） | CEG8BR | RRF C | B3A8 |
| 转换为定点（短HFP到32位） | CEFR | RRF C | B3B8 |
| 转换为定点（短HFP到64位） | CEG8R | RRF C | B3C8 |
| 将Unicode转换为UTF-8 | CUUTF | RRE C | B2A6 |

