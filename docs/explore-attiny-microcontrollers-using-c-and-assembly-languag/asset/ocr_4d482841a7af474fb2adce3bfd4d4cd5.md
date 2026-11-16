Bits that are found in the status register or SREG are defined in the header file for the AVR being used. These names can be used with the BRBS and BRBC instructions, and are shown as they appear in the header file below.

```
; SREG - Status Register
.equ SREG_C = 0 ; Carry Flag
.equ SREG_Z = 1 ; Zero Flag
.equ SREG_N = 2 ; Negative Flag
.equ SREG_V = 3 ; Two's Complement Overflow Flag
.equ SREG_S = 4 ; Sign Bit
.equ SREG_H = 5 ; Half Carry Flag
.equ SREG_T = 6 ; Bit Copy Storage
.equ SREG_I = 7 ; Global Interrupt Enable
```

BRBS is the counterpart to BRBC. While BRBC checks if a status register bit is clear, BRBS checks if a status register bit is set. The other branch instructions that follow are synonyms for BRBS and BRBC, and are typically used after one of the compare instructions.

# Branch if Equal or Not Equal – SREG Z Flag

+   **BREQ (Branch if Equal)**
+   Equivalent to BRBS SREG_Z,k where k is the constant relative address to branch to.
+   
+   **BRNE (Branch If Not Equal)**
+   Equivalent to BRBC SREG_Z,k where k is the constant relative address to branch to.

# Branch if Carry Set or Cleared – SREG C Flag

+   **BRCS (Branch if Carry Set)**
+   Equivalent to BRBS SREG_C,k where k is the constant relative address to branch to.
+   
+   **BRCC (Branch if Carry Cleared)**
+   Equivalent to BRBC SREG_C,k where k is the constant relative address to branch to.

# Branch if Same or Higher, or Lower – SREG C Flag

+   **BRSH (Branch if Same or Higher (Unsigned))**
+   Equivalent to BRCC SREG_C,k where k is the constant relative address to branch to.
+   
+   **BRLO (Branch if Lower (Unsigned))**
+   Equivalent to BRBS SREG_C,k where k is the constant relative address to branch to.