

```assembly
CLRF SIGN2 ; Clear [SIGN2] to 0 ; STEPS 1 AND 2 OF THE ALGORITHM OF SECTION 7.7.1
BTFSs MULT1, 7 ; Check sign bit 7 for 1 for 1st #
BRA NEG ; If sign = 0, branch to check sign of 2nd #
INCF SIGN1 ; Increment [SIGN1] if sign of 1st# = 1
NEGF MULT1 ; and take 2's complement of [MULT1]
NEG
BTFSs MULT2, 7 ; Check sign bit 7 for 1 for 2nd #
BRA POSMUL ; If both sign = 0, branch for unsigned mul
INCF SIGN2 ; Increment [SIGN2] if sign of 2nd # = 1
NEGF MULT2 ; and take 2's complement of [MULT2]
; STEP 3 OF THE ALGORITHM OF SECTION 7.7.1
POSMUL
MOVF MULT1, W ; Move [MULT1] to WREG
MULWF MULT2 ; Unsigned product in PRODH:PRODL
MOVF SIGN1, W ; Move [SIGN1] to WREG
XORWF SIGN2 ; Compute sign of the result
BTFSs SIGN2, 0 ; If sign of result is 0, result in
BRA FINISH ; PRODH:PRODL and Stop
COMF PRODL ; For negative result, take comp of PROD
; STEPS 4 AND 5 OF THE ALGORITHM OF SECTION 7.7.1
COMF PRODH ; Take 2's complement of PRODL
MOVLW 1
ADDWF PRODL
MOVLW 0
ADDWF PRODH, F ; Result in PRODH:PRODL in 2's comp
FINISH
SLEEP
END
```

## 7.7.2 无符号除法算法

8 位乘以 8 位的无符号除法可以使用重复减法算法来执行。例如，考虑如下将 $7_{10}$ 除以 $3_{10}$：

| 被除数 | 除数 | 减法结果 | 计数器 |
|---|---|---|---|
| $7_{10}$ | $3_{10}$ | 7 - 3 = 4 | 1 |
| 4 - 3 = 1 | | 1 + 1 = 2 | 2 |

商 = 计数器值 = 2，余数 = 减法结果 = 1。

在此，每当减法结果大于除数时，计数器加一。一旦减法结果小于除数，即可获得结果。无符号除法算法可以总结如下：

首先，将被除数和除数加载到数据寄存器中，并将计数器初始化为 0 以保存商（除数可以被减去的次数，直到减法结果小于除数为止）。存储被除数的数据寄存器最终将包含商（减法结果）。可以使用数值数据来验证该算法。

- 1. 比较被除数与除数是否相等。
- 2. 如果相等，计数器加 1，然后执行（被除数 - 除数）。将减法结果存储在保存被除数的数据寄存器中。如果不相等，转到步骤 3。
- 3. 比较被除数是否大于除数。如果大于，计数器加 1，然后执行（被除数 - 除数）。将减法结果存储在保存被除数的数据寄存器中。
- 4. 转到步骤 1，并重复步骤 1 至 3，直到减法结果小于或等于 0。
- 5. 当被除数中的减法结果小于或等于除数时，转到停止。计数器将包含商（除数可以被减去的次数，直到减法结果小于除数为止）。保存被除数的数据寄存器将包含余数（减法结果）。

示例 7.5 使用刚刚描述的无符号除法算法，希望将存储在数据寄存器 0x20 中的 8 位无符号数（被除数）除以存储在数据寄存器 0x30 中的另一个 8 位无符号数（除数）。将 16 位结果保存在数据寄存器 0x71（余数高字节）和 0x70（商低字节）中。

(a) 将该问题绘制成流程图。

(b) 将流程图转换为从地址 0x100 开始的 PIC18F 汇编语言程序。

### 解答

(a)

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_190_0.png)

(b)

```assembly
                INCLUDE <P18F4321.INC>
                ORG        0x100
DIVIDEND EQU     0x20
DIVISOR EQU      0x21
COUNTER EQU      0x30
                MOVWF    16        ; Dividend in WREG
                MOVWF DIVIDEND     ; Store dividend in 0x20
                MOVWF    4          ; Divisor in WREG
                MOVWF DIVISOR      ; Store divisor in 0x21
                CLRF COUNTER       ; Clear Counter to 0
; STEPS 1 AND 2 OF THE ALGORITHM OF SECTION 7.7.2
BACK           CPFSEQ DIVIDEND     ; If dividend equals divisor, skip next instr.
                BRA    RESULT       ; If not equal, branch to RESULT
                INCF COUNTER, F    ; Increment [0x20] by 1
                SUBWF DIVIDEND, F  ; Subtract divisor from dividend, result in 0x20
                BRA    FOREVER      ; Go to Halt
; STEPS 3, 4 AND 5 OF THE ALGORITHM OF SECTION 7.7.2
RESULT         CPFSGT DIVIDEND     ; If dividend greater than divisor, skip next inst.
                BRA    FOREVER      ; Quotient in 0x30, Remainder in 0x20, halt
                INCF COUNTER, F    ; Increment [0x20] by 1
                SUBWF DIVIDEND, F  ; Subtract divisor from dividend, result in 0x20
                BRA    BACK         ; Repeat
FOREVER        GOTO FOREVER        ; Halt
                END
```

## 7.7.3 有符号除法算法

8 位乘以 8 位的有符号除法算法使用除法方程：
被除数 = 商 × 除数 + 余数

可以使用多种算法执行有符号除法。一种简单的算法如下。假设 DV（被除数）和 DR（除数）处于补码形式。对于第一种情况，使用不带符号位的幅值进行无符号除法的重复减法。商的符号位由 $DV_n \oplus DR_n$ 确定，其中 $DV_n$ 和 $DR_n$ 分别是被除数（DV）和除数（DR）的最高有效位（符号位）。执行有符号除法时，按如下步骤进行：

- 1. 如果 $DV_n$ = 1，计算 DV 的补码，否则保持 DV 不变。
- 2. 如果 $DR_n$ = 1，计算 DR 的补码，否则保持 DR 不变。
- 3. 使用无符号除法算法（重复减法）将被除数的 $n$ - 1 位除以除数。
- 4. 商的符号，$Q_n$ = $DV_n \oplus DR_n$。余数的符号与被除数的符号相同，除非余数为零。
- 5. 如果 $Q_n$ = 1，计算步骤 3 中获得的商的补码，否则保持商不变。

**示例 7.6** 在地址 0x100 处编写一个 PIC18F 汇编语言程序，将寄存器 0x30 中的 8 位有符号数（被除数）除以寄存器 0x40 中的另一个 8 位有符号数（除数）。使用上一节中描述的有符号除法算法。

### 解答

```assembly
INCLUDE <P18F4321.INC>
ORG        0x100
COUNTER EQU    0x20
DIVIDEND EQU   0x30
DIVISOR EQU    0x40
SIGN1  EQU    0x50
SIGN2  EQU    0x51

MOVLW    4    ; Load 8-bit data (+4) in WREG
MOVWF    DIVIDEND    ; Save in DIVIDEND
MOVLW    0xFE    ; Load 8-bit data (-2) in WREG
MOVWF    DIVISOR    ; Save in DIVISOR
CLRF    SIGN1    ; Clear [SIGN1] to 0
CLRF    SIGN2    ; Clear [SIGN2] to 0
; STEPS 1 AND 2 OF THE ALGORITHM OF SECTION 7.7.3

BFSS    DIVIDEND, 7    ; Check sign bit 7 for 1 for 1st #
BRA    NEG    ; If sign = 0, branch to check sign of 2nd #
INCF    SIGN1    ; Increment [SIGN1] if sign of 1st # = 1
NEG    NEGF    DIVIDEND    ; take 2's complement of [DIVIDEND]
BFSS    DIVISOR, 7    ; Check sign bit 7 for 1 for [DIVISOR]
BRA    POSDIV    ; If both signs = 0, branch for unsigned division
INCF    SIGN2    ; Increment [SIGN2] if sign of 2nd # = 1
NEG    NEGF    DIVISOR    ; and take 2's complement of [DIVISOR]
; STEP 3 OF THE ALGORITHM OF SECTION 7.7.3

POSDIV    MOVF    DIVISOR, W    ; Load divisor into WREG
CLRF    COUNTER    ; Clear Counter to 0
BACK    CPFSEQ    DIVIDEND    ; If dividend equals divisor, skip next instr.
BRA    RESULT1    ; If not equal, branch to RESULT
INCF    COUNTER, F    ; Increment [0x20] by 1
SUBWF    DIVIDEND, F    ; Subtract divisor from dividend, result in 0x20
RESULT1 CPFSGT    DIVIDEND    ; If dividend greater than divisor, skip next inst.
BRA    RESULT    ; Quotient in 0x20, Remainder in 0x30
INCF    COUNTER, F    ; Increment [0x20] by 1
SUBWF    DIVIDEND, F    ; Subtract divisor from dividend, result in 0x30
BRA    BACK    ; Repeat
; STEPS 4 AND 5 OF THE ALGORITHM OF SECTION 7.7.3

RESULT    MOVF    SIGN1, W    ; Move [SIGN1] to WREG
XORWF    SIGN2    ; Compute sign of the result
BFSS    SIGN2, 0    ; If sign of the quotient is 0, result in 0x70 and Stop
BRA    FINISH
NEGF    0x20    ; For negative result, take comp of [0x20]
BFSS    SIGN1, 0    ; Check sign of DIVIDEND
BRA    FINISH    ; If plus, positive remainder in 0x30
FINISH    NEGF    0x30    ; If negative, negate remainder in 0x30
END
```

