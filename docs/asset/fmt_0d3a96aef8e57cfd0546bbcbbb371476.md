
```c
printf(" LR = %08X\r\n", frame->lr);

printf(" PC = %08X\r\n", frame->pc);

printf(" PSR = %08X\r\n", frame->psr);

printf("FSR/FAR: %r\n");

printf(" CFSR = %08X\r\n", csfr);

printf(" HFSR = %08X\r\n", SCB->HFSR);

printf(" DFSR = %08X\r\n", SCB->DFSR);

printf(" AFSR = %08X\r\n", AFSR);

if (csfr & (1 << 7)) {

    printf(" MMFAR = %08X\r\n", mmfar);

}

if (csfr & (1 << 15)) {

    printf(" BFAR = %08X\r\n", bfar);

}

printf("Misc%r\n");

printf(" LR/EXEC_RETURN = %08X\r\n", lr);

}

void HardFault_Handler(void) {

    asm tst lr, #4 \r\n

    ite eq \r\n

    mrseq r0,msp \r\n

    mrne r0,psp \r\n

    mov r1,lr \r\n

    ldr r2=HardFault_Handler_C \r\n

    bx r2;

    /* Outputs */

    /* Inputs */

    /* Clobbers */

}

void HardFault_Handler_C(ExceptionStackFrame* frame,

    uint32_t lr) {

    uint32_t mmfar = SCB->MMFAR; // MemManage Fault Address

    uint32_t bfar = SCB->BFAR; // Bus Fault Address

    uint32_t cfsr = SCB->CFSR; // Configurable Fault Status Registers

    printf("[HardFault]\r\n");

    dumpExceptionStack(frame, cfsr, mmfar, bfar, lr);

#if defined(DEBUG)

    __BKPT();

#endif

    while (1);

}
```
