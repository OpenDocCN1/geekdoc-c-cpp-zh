+   1. Clear INTxIF for each interrupt to 0. These flags will be set to ones automatically after occurrence of interrupts. Note that INT01F is located in the INTCON register while INT1IF and INT2IF are located in INTCON3 register.
2. Set INTxE for each interrupt to 1. Note that INT0IE is located in the INTCON register while the INT1IE and INT2IE are contained in the INTCON3 register.
3. Set the GIE (Global Interrupt Enable) bit in the INTCON register to 1.
4. Finally, since the external interrupts (INT0-INT2) are multiplexed with analog inputs (AN8, AN10, and AN12), the ADCON1 register must be configured as digital input.

Next, consider INT0 in Figure 9.8. According to the steps listed above, the following initializations in PIC18F assembly language are necessary before the PIC18F will be able to accept external interrupt via its INT0 pin:

```
BCF     INTCON, INT0IF    ; Clear INT0IF to 0
BSF     INTCON, INT0IE    ; Set INT0IE to 1
BSF     INTCON, GIE       ; Set GIE to 1
MOVLW   0x0F            ; Configure INT0-INT2 as digital inputs
MOVWF   ADCON1
```

The C-equivalent of the above PIC18F assembly language will be:

```
INTCONbits.INT0IF = 0;    // Clear INT0IF to 0
INTCONbits. INT0IE = 1;   // Set INT0IE to 1
INTCONbits. GIE = 1;      // Set GIE to 1
ADCON1 = 0x0F;            // Configure INT0-INT2 as digital inputs
```

In Figure 9.8, the above PIC18F instruction sequence or C-statements will send a ‘0’ to the output of AND gate #1. This is because INT0IF = 0, INT0IE = 1, and GIE = 1; note that INT1IE and INT2IE are zero after reset. This, in turn, will make the output of AND gate #5 as 0. As soon as the PIC18F is interrupted via the INT0 pin, the PIC18F completes the current instruction, pushes the current contents of the program counter (Return address) onto the stack, and then automatically sets the INT0IF to 1. Hence, the output of AND gate #5 will be ‘1’ in Figure 9.8, and the PIC18F will load address 0x00008 into the program counter, and thus branches to the interrupt service routine.

The following PIC18F assembly instruction sequence will enable all external interrupts:

```
BCF     INTCON, INT0IF    ; INT0IF = 0
BCF     INTCON3, INT1IF   ; INT1IF = 0
BCF     INTCON3, INT2IF   ; INT2IF = 0
BSF     INTCON, INT0IE    ; Enable INT0
BSF     INTCON3, INT1IE   ; Enable INT1
BSF     INTCON3, INT2IE   ; Enable INT2
BSF     INTCON, GIE       ; Enable GIE
MOVLW   0x0F            ; Configure INT0-INT2
MOVWF   ADCON1          ; as digital inputs
```

The following C-language statements will enable all external interrupts:

```
INTCONbits.INT0IF=0;     // INT0IF = 0
INTCON3bits.INT1IF=0;    // INT1IF = 0
```