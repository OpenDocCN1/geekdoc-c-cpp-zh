
## TSTFSZ Test f, Skip if 0

**Syntax:**
TSTFSZ f(a)

**Operands:**
0 ≤ f ≤ 255
a = [0,1]

**Operation:**
skip if f = 0

**Status Affected:**
None

| Binary | Binary | Hex | Hex |
| :--- | :--- | :--- | :--- |
| 0110 | 011a | ffff | ffff |

**Description:**
If ‘f = 0’, the next instruction fetched during the current instruction execution is discarded and a NOOP is executed, making this a two-cycle instruction.
If ‘a’ is ‘0’, the Access Bank is selected.
If ‘a’ is ‘1’, the BSR is used to select the GPR bank (default).
If ‘a’ is ‘0’ and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f ≤ 95 (5Fh). See Section 24.2.3 “Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode” for details.

**Words:**
1

**Cycles:**
1(2)

**Note:**
3 cycles if skip and followed by a 2-word instruction.

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read register ‘f’ | Process Data | No operation |

If skip:

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |

If skip and followed by 2-word instruction:

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |
| No operation | No operation | No operation | No operation |

```
Example:
HERE TSTFSZ CNT, 1
NZERO :
ZERO :

Before Instruction
PC = Address (HERE)
After Instruction
If CNT = 00h,
PG = Address (ZERO)
If CNT ≠ 00h,
PG = Address (NZERO)
```

## XORLW Exclusive OR Literal with W

**Syntax:**
XORLW k

**Operands:**
0 ≤ k ≤ 255

**Operation:**
(W).XOR. k → W

**Status Affected:**
N, Z

| Binary | Binary | Hex | Hex |
| :--- | :--- | :--- | :--- |
| 0000 | 1010 | kkkk | kkkk |

**Description:**
The contents of W are XORed with the 8-bit literal ‘k’. The result is placed in W.

**Words:**
1

**Cycles:**
1

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read literal ‘k’ | Process Data | Write to W |

```
Example:
XORLW 0AFh
Before Instruction W = B5h
After Instruction W = 1Ah
```

## XORWF Exclusive OR W with f

| | |
| :--- | :--- |
| **Syntax:** | `XORWF f {,d {,a}}` |
| **Operands:** | `0 <= f <= 255`<br>`d ∈ [0,1]`<br>`a ∈ [0,1]` |
| **Operation:** | `(W),XOR, (f) -> dest` |
| **Status Affected:** | N, Z |
| **Encoding:** | `0001 10da ffff ffff` |
| **Description:** | Exclusive OR the contents of W with register ‘f’. If ‘d’ is ‘0’, the result is stored in W. If ‘d’ is ‘1’, the result is stored back in the register ‘f’ (default).<br> If ‘a’ is ‘0’, the Access Bank is selected.<br> If ‘a’ is ‘1’, the BSR is used to select the GPR bank (default).<br> If ‘a’ is ‘0’ and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f ≤ 95 (5Fh). See **Section 24.2.3 “Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode”** for details. |

**Words:** 1

**Cycles:** 1

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
| :---: | :---: | :---: | :---: |
| Decode | Read register ‘f’ | Process Data | Write to destination |

**Example:**

```
XORWF REG, 1, 0

Before Instruction
REG = AFh
W = B5h
After Instruction
REG = 1Ah
W = B5h
```

## APPENDIX E: PIC18F4321 SPECIAL FUNCTION REGISTERS

**SPECIAL FUNCTION REGISTERS**
The Special Function Registers (SFRs) are registers used by the CPU and peripheral modules for controlling the desired operation of the device. These registers are implemented as static RAM. SFRs start at the top of data memory (FFFh) and extend downward to occupy the top half of Bank 15 (F80h to FFFh). A list of these registers is given in Table E-1.

### TABLE E-1: SPECIAL FUNCTION REGISTER MAP FOR PIC18F4321 FAMILY DEVICES

| Address | Name | Address | Name | Address | Name | Address | Name |
|---|---|---|---|---|---|---|---|
| FFFh | TOSU | FDCh | INDF2${}^{(1)}$ | FBFh | CCPRIH | F9Fh | IPR1 |
| FFEh | TOSH | FDCh | POSTINC2${}^{(1)}$ | FBEh | CCPRIOL | F9Dh | PIR1 |
| FFDh | TOSL | FDDh | POSTDEC2${}^{(1)}$ | FBDh | CCP1CON | F9Ch | PIE1 |
| FFC h | STKPTR | FDC h | PREINC2${}^{(1)}$ | FBC h | CCPR2H | F9Ch | __${}^{(2)}$ |
| FFB h | CLATH | FDB h | PLUSW2${}^{(1)}$ | FBB h | CCPR2L | F9Ch | OSCRUNE |
| FFAh | PCLATH | FADh | FSR2L | FBAh | CCPR2CON | F9Ah | __${}^{(2)}$ |
| FF9h | PCL | FD9h | FSR2L | F99h | __${}^{(2)}$ | F99h | __${}^{(2)}$ |
| FF8h | TBLPTRU | FD8h | STATUS | F88h | BAUDCON | F98h | __${}^{(2)}$ |
| FF7h | TBLPTRH | FD7h | TMR0H | F87h | ECCP1DEL${}^{(3)}$ | F97h | __${}^{(2)}$ |
| FF6h | TBLPTRL | FD6h | TMR0L | F86h | ECCP1AS${}^{(3)}$ | F96h | TRISF${}^{(3)}$ |
| FF5h | TABLAT | FD5h | T0CON | F85h | CVRCON | F95h | TRISD${}^{(3)}$ |
| FF4h | PRODH | FD4h | __${}^{(2)}$ | F84h | CMCON | F94h | TRISC |
| FF3h | PRODL | FD3h | OSCCON | F83h | TMR3H | F93h | TRISB |
| FF2h | INTCON | FD2h | HVLVDCON | F82h | TMR3L | F92h | TRISA |
| FF1h | INTCON2 | FD1h | WDTCON | F81h | T3CON | F91h | __${}^{(2)}$ |
| FF0h | INTCON3 | FD0h | RCON | F80h | SPBRGH | F90h | __${}^{(2)}$ |
| FEFh | INDF0${}^{(1)}$ | FCFh | TMR1H | FA7h | SPBRG | F87h | __${}^{(2)}$ |
| FEEh | POSTINC0${}^{(1)}$ | FCC h | TMR1L | FAEh | RCGR | F8Eh | __${}^{(2)}$ |
| FEDh | POSTDEC0${}^{(1)}$ | FCDh | T1CON | FAdh | TXREG | F8Dh | LATE${}^{(3)}$ |
| FECh | PREINC0${}^{(1)}$ | FCC h | TMR2 | FACH | TXSTA | F8Ch | LATD${}^{(3)}$ |
| FEBh | PLUSW0${}^{(1)}$ | FCB h | PR2 | FAbh | RCSTA | F8Bh | LATIC |
| FEAh | FSR0H | FCAh | T2CON | FAAh | __${}^{(2)}$ | F8Ah | LATB |
| FE9h | FSR0L | FC9h | SSPBUF | FA9h | EEADR | F89h | LATA |
| FE8h | WREG | FC8h | SSPADD | FA8h | EEDATA | F88h | __${}^{(2)}$ |
| FE7h | INDF1${}^{(1)}$ | FC7h | SSPSTAT | FA7h | EECON2${}^{(1)}$ | F87h | __${}^{(2)}$ |
| FE6h | POSTINC1${}^{(1)}$ | FC6h | SSPCON1 | FA6h | EECON1 | F86h | __${}^{(2)}$ |
| FE5h | POSTDEC1${}^{(1)}$ | FC5h | SSPCON2 | FA5h | __${}^{(2)}$ | F85h | __${}^{(2)}$ |
| FE4h | PREINC1${}^{(1)}$ | FC4h | ADRESL | FA4h | __${}^{(2)}$ | F84h | PORTE${}^{(3)}$ |
| FE3h | PLUSW1${}^{(1)}$ | FC3h | ADRESL | FA3h | __${}^{(2)}$ | F83h | PORTD${}^{(3)}$ |
| FE2h | FSR1H | FC2h | ADCON0 | FA2h | IPR2 | F82h | PORTC |
| FE1h | FSR1L | FC1h | ADCON1 | FA1h | PIR2 | F81h | PORTB |
| FE0h | BSR | FC0h | ADCON2 | FA0h | PIE2 | F80h | PORTA |

**Note 1:** This is not a physical register.
**2:** Unimplemented registers are read as '0'.
**3:** This register is not available on 28-pin devices.

## APPENDIX F: TUTORIAL FOR ASSEMBLING AND DEBUGGING A PIC18F ASSEMBLY LANGUAGE PROGRAM USING THE MPLAB

The PIC18F assembly language programs in this book are assembled using Microchip MPLAB assembler. Appendix F provides a tutorial showing step-by-step procedure to download the MPLAB assembler from Microchip’s website (www.microchip.com), and assemble a simple PIC18F assembly language program using MPLAB IDE v8.50. Microchip introduces newer versions of the MPLAB assembler frequently. One may download the MPLAB IDE v8.50 from the archive from Microchip website.

### Assembling PIC18F assembly language program using MPLAB

First, download MPLAB IDE v8.50 from the Microchip website as follows:

1. Go to www.microchip.com.
2. Type in MPLAB IDE v8.50 in the “search” and hit return.
3. Click on MPLAB IDE v8.50.

After installing and downloading the program, you will see the following icon on your desktop:

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_438_0.png)

Double click (right) on the MPLAB icon and wait until you see the following screen:

Next, click on ‘Project’ and then ‘Project Wizard’; the following screen will appear:

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_439_0.png)

Click Next; the following screen shot will be displayed:

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_440_0.png)

Select the device PIC18F4321, hit Next, and wait; the following will be displayed:

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_441_0.png)

In the ‘Active Toolsuite’, select ‘Microchip MPASM Toolsuite’, and click Next; the following will be displayed:

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_442_0.png)

Select a location where all project contents will be placed. For this example, the folder will be placed on the desktop (arbitrarily chosen). Go to the desktop directory, make a new folder, and name the folder. In order to do this, click on “Browse”, and select desktop:

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_442_1.png)
