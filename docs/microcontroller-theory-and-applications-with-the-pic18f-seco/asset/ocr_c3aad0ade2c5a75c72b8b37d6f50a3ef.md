As mentioned before, upon power-on reset, the interrupt address vector is 0x000008 (default), and no interrupt priorities are available. Also, upon power-on reset, IPEN is automatically cleared to 0, and the PIC18F operates as a high-priority interrupt (single interrupt) system. Hence, the interrupt vector address is 0x000008. The IPEN bit (bit 7 of the RCON register) of the RCON register in Figure 8.6 can be programmed to assign interrupt priorities. During normal operation, the IPEN bit can be set to one by executing the "BSF RCON, IPEN" in PIC18F assembly or "RCONbits.IPEN = 1;" in C-language to assign priorities in the system.

When interrupt priority is enabled (IPEN = 1), there are two bits which enable interrupts globally. Setting the GIEH bit (bit 7 of INTCON register of Figure 9.7(a)) enables all interrupts that have the priority bit set (high priority). Setting the GIEL bit (bit 6 of INTCON register of Figure 9.7(a)) enables all low interrupts. When the interrupt flag, interrupt enable bit and appropriate global interrupt enable bit are set, the interrupt will vector immediately to address 0x000008 or 0x000018, depending on the priority bit setting. Individual interrupts can be disabled through their corresponding enable (INTxIE) bits.

From Figure 9.7(a), when IPEN of RCON register is 0, bits 6 and 7 of the INTCON register become GIE (Global Interrupt Enable) bit and PEI (Peripheral Interrupt Enable) bit. Setting or cleaning the GIE bit via programming will enable or disable all interrupts (INT0, INT1, INT2). On the other hand, setting or clearing the PEIE bit will enable or disable all peripheral interrupts.

Table 9.1 shows the three external interrupts of the PIC18F4321 along with the corresponding Interrupt Priority (IP) bit.

As shown in the table, since an IP (Interrupt Priority) is not assigned to INT0, it always has the high priority level. However, INT1 and INT2 can be programmed as high or low level priorities. When INT1 and INT2 are used as two interrupts in an application; INT0 is not used. For example, in order to program INT1 as a high priority interrupt and INT2 as a low priority interrupt, the following PIC18F assembly language instruction sequence can be used:

![](bbox=[0.16, 0.585, 0.92, 0.65])

+   bit 7 **RBPU**: PORTB Pull-up Enable bit
1 = All PORTB pull-ups are disabled
0 = PORTB pull-ups are enabled by individual port latch values
bit 6 **INTEDG0**: External Interrupt 0 Edge Select bit, 1 = Interrupt on rising edge, 0 = Interrupt on falling edge
bit 5 **INTEDG1**: External Interrupt 1 Edge Select bit, 1 = Interrupt on rising edge, 0 = Interrupt on falling edge
bit 4 **INTEDG2**: External Interrupt 2 Edge Select bit, 1 = Interrupt on rising edge, 0 = Interrupt on falling edge
bit 3 **Unimplemented**: Read as '0'
bit 2 **TMROIP**: TMR0 Overflow Interrupt Priority bit, 1 = High priority, 0 = Low priority
bit 1 **Unimplemented**: Read as '0'
bit 0 **RBIP**: RB Port Change Interrupt Priority bit, 1 = High priority, 0 = Low priority

# **FIGURE 9.9** INTCON2 Register