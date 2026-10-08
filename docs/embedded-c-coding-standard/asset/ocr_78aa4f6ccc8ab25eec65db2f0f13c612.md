# 5.5 Structures and Unions

Rules:

+   a. Appropriate care shall be taken to prevent the compiler from inserting padding bytes within struct or union types used to communicate to or from a peripheral or over a bus or network to another processor.

+   b. Appropriate care shall be taken to prevent the compiler from altering the intended order of the bits within bit-fields.

Example:

```
typedef struct {
    uint16_t  count;      // offset 0
    uint16_t  max_count;  // offset 2
    uint16_t  unused;     // offset 4

    uint16_t  enable      : 2;   // offset 6 bits 15-14
    uint16_t  b_interrupt : 1;   // offset 6 bit 13
    uint16_t  _unused1   : 7;   // offset 6 bits 12-6
    uint16_t  b_complete : 1;   // offset 6 bit 5
    uint16_t  _unused2   : 4;   // offset 6 bits 4-1
    uint16_t  b_periodic : 1;   // offset 6 bit 0
} timer_reg;
```

```
// Preprocessor check of timer register layout byte count.
#if (8 != sizeof(timer_reg))
# error "timer_reg_t struct size incorrect (expected 8 bytes)"
#endif
```