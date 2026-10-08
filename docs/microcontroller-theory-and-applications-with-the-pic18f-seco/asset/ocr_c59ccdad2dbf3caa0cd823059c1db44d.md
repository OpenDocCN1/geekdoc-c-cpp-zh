Appendix C: PIC18F Instruction Set (Alphabetical Order)

385

| Instruction | Example | Operation |
| :--- | :--- | :--- |
| DECFSZ F, d, a | DECFSZ 0x30, W | Decrement [0x30] by 1, and store result in WREG. If [WREG] = 0, skip the next instruction; else, execute the next instruction. |
| | DECFSZ 0x30, F | Decrement [0x30] by 1, and store the result in 0x30. If [0x30] = 0, skip the next instruction; else, execute the next instruction. |
| DECFSNZ F, d, a | DECFSNZ 0x50, W | Decrement [0x50] by 1, and store result in WREG. If [WREG] $\neq$ 0, skip the next instruction; else, execute the next instruction. |
| | DECFSNZ 0x50, F | Decrement [0x50] by 1, and store the result in 0x50. If [0x50] $\neq$ 0, skip the next instruction; else, execute the next instruction. |
| GOTO k | GOTO START | Unconditional branch to address *START*. |
| INCF F, d, a | INCF 0x20, W | Increment [0x20] by 1, and store result in WREG. |
| | INCF 0x20, F | Increment [0x20] by 1, and store result in 0x20. |
| INCFSZ F, d, a | INCFSZ 0x30, W | Increment [0x30] by 1, and store result in WREG. If [WREG] = 0, skip the next instruction; else, execute the next instruction. |
| | INCFSZ 0x30, F | Increment [0x30] by 1, and store the result in 0x30. If [0x30] = 0, skip the next instruction; else, execute the next instruction. |
| INCFSNZ F, d, a | INCFSNZ 0x50, W | Increment [0x50] by 1, and store result in WREG. If [WREG] $\neq$ 0, skip the next instruction; else, execute the next instruction. |
| | INCFSNZ 0x50, F | Increment [0x50] by 1, and store the result in 0x50. If [0x50] $\neq$ 0, skip the next instruction; else, execute the next instruction. |
| IORLW k | IORLW 0x54 | The contents of WREG are logically ORed with 0x54, and the result is stored in WREG. |