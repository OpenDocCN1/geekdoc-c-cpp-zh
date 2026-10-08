The MOVWF 0x50 instruction moves the contents of the WREG register into a file register in the data SRAM whose address is 0x50. The contents of WREG are unchanged. MOVWF 0x50 uses direct address mode since address 0x50 is directly specified in the MOVWF instruction.

Note that the 12-bit address, 0x050 in the access bank, is specified by 8-bit number 0x50 in the MOVWF instruction since the upper four bits (0H) of the 12-bit address 0x050 specify the bank number 0 (access bank) in this case. The 8-bit address (0x50) is included in the MOVWF (16-bit wide) instruction. As mentioned before, in the PIC18F, addresses are specified as 8-bit numbers while the bank number is specified by the access bank or BSR.

# ### 5.4.4 Indirect Addressing Mode

In *Indirect Addressing Mode*, a register is used as a pointer to an address in the data memory. In the PIC18F, three registers, namely FSR0, FSR1, and FSR2 are used for this purpose. Note that “FSR” stands for file select register. The PIC18F CPU contains these registers. As mentioned before, each of these 16-bit registers is divided into low byte and high byte as follows: FSR0 as FSR0H and FSR0L, FSR1 as FSR1H and FSR1L, FSR2 as FSR2H and FSR2L. Each of these registers holds a 12-bit memory address to point to a data memory location. Since FSR’s are 16-bit wide, the 12-bit address is stored in low 12 bits (bits 0 through 11) of the FSRs with the upper four bits (bits 12 through 15) as 0’s.

Each FSR is associated with an SFR (Special Function Register) called INDF (Indirect File) as follows: FSR0 is associated with SFR called INDF0, FSR1 is associated with SFR called INDF1, and FSR2 is associated with SFR called INDF2. The FSR’s can be initialized using the LFSR (Load FSR) instruction. The following examples illustrate this:

```
LFSR    0, 0x00010    ; Load  0010H into FSR0
LFSR    1, 0x0040     ; Load  0040H into FSR1
LFSR    2, 0x0080     ; Load  0080H into FSR2
```

After initializing one of the FSR’s, data can be moved into a RAM location indirectly using the associated SFR called INDF. For example, in order to move the

![](bbox=[0.2, 0.6, 0.6, 0.75])

(a) Memory contents after execution of MOVLW and LFSR instructions in the example for indirect addressing

![](bbox=[0.2, 0.77, 0.6, 0.9])

(b) Memory contents after execution of MOVWF in the example for indirect addressing

**FIGURE 5.8** Illustration of the Indirect Addressing Mode