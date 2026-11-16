# 10.2.2.3 Timing of the Code

Now that we understand the basic working of the wait_1s subroutine, we can examine the timing of the instructions used in this subroutine. The code is repeated below, showing the number of clock cycles used by each instruction

```
wait_1s:
ldi    R16, low  ((F_CPU - 10) / 10)   ; 1 clock cycle
ldi    R17, byte2((F_CPU - 10) / 10)   ; 1 clock cycle
ldi    R18, byte3((F_CPU - 10) / 10)   ; 1 clock cycle
ldi    R19, byte4((F_CPU - 10) / 10)   ; 1 clock cycle

wait_is_loop:
subi   R16, 1                          ; 1 clock cycle
sbci   R17, 0                          ; 1 clock cycle
sbci   R18, 0                          ; 1 clock cycle
sbci   R19, 0                          ; 1 clock cycle
mov    R20, R16                        ; 1 clock cycle
or     R20, R17                        ; 1 clock cycle
or     R20, R18                        ; 1 clock cycle
or     R20, R19                        ; 1 clock cycle
brbc   SREG_Z, wait_is_loop            ; 1 clock cycles
nop                                  ; 1 clock cycle
nop                                  ; 1 clock cycle
nop                                  ; 1 clock cycle
ret                                  ; 4 clock cycles
```

As can be seen in the code, every instruction takes only one clock cycle, except for the BRBC instruction and the RET instruction. As we know, the BRBC instruction takes two clock cycles when it branches to the top of the loop, and one clock cycle when it does not branch. In order to effectively make this instruction always use up two clock cycles, a single NOP instruction is placed below it. This means that when BRBC does not branch, it executes the NOP instruction below it effectively using up two clock cycles instead of one.

Instructions in the loop, shown in bold in the above listing, add up to 10 clock cycles. The NOP instruction directly below BRBC is included in this total, as it effectively causes the final execution of BRBC to still use up two clock cycles. F_CPU must be divided by these 10 clock cycles before being loaded into R16 to R19 at the top of the subroutine. This is because the subtraction process in the loop uses up these 10 clock cycles and the subroutine would therefore take 10 times longer if we did not compensate for these 10 clock cycles.

Besides the clock cycles used in the loop, there are clock cycles used before and after the loop. Four clock cycles are used by the LDI instructions at the beginning of the wait_1s