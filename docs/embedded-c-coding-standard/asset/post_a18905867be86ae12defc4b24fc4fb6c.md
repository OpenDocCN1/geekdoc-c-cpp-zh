
## 8.5 Jumps

Rules:

- a. The use of goto statements shall be restricted as per Rule 1.7.c.
- b. C Standard Library functions abort(), exit(), setjmp(), and longjmp() shall not be used.

Reasoning: Algorithms that utilize jumps to move the instruction pointer can and should be rewritten in a manner that is more readable and thus easier to maintain.

Enforcement: These rules shall be enforced by an automated scan of all modified or new modules for inappropriate use of forbidden tokens. To the extent that the use of goto is permitted, code reviewers should investigate alternative code structures to improve code maintainability and readability.

## Embedded C Coding Standard

## 8.6 Equivalence Tests

Rules:

- When evaluating the equality of a variable against a constant, the constant shall always be placed to the left of the equal-to operator (==).

Example:

```c
if (NULL == p_object)
{
    return (ERR_NULL_PTR);
}
```

Reasoning: It is always desirable to detect possible typos and as many other coding defects as possible at compile-time. Defect discovery in later phases is not guaranteed and often also more costly. By following this rule, any compiler will reliably detect erroneous attempts to assign (i.e., = instead of ==) a new value to a constant.

Enforcement: Many compilers can be configured to warn about suspicious assignments (i.e., located where comparisons are more typical). However, ultimate responsibility for enforcement of this rule falls to code reviewers.

![](img/25b91ff016aae4a7e187afd99b37dc2d_67_0.png)

## Appendix A: Table of Abbreviations

The following abbreviations and acronyms are accepted for use in source code without local explanation.

| max | Meaning |
|---|---|
| adc | analog-to-digital converter |
| avg | average |
| b_ | Boolean |
| buf | buffer |
| cfg | configuration |
| curr | current (item in a list) |
| dac | digital-to-analog converter |
| ee | EEPROM |
| err | error |
| g_ | global |
| gpio | general-purpose I/O pins |
| h_ | handle (to) |
| init | initialize |
| io | input/output |
| isr | interrupt service routine |
| lcd | liquid crystal display |
| led | light-emitting diode |
| max | maximum |
| mbox | mailbox |
| mgr | manager |
| min | minimum |

| msec | millisecond^1 |
| --- | --- |
| msg | message |
| next | next (item in a list) |
| nsec | nanosecond |
| num | number (of) |
| p_ | pointer (to) |
| pp_ | pointer to a pointer (to) |
| prev | previous (item in a list) |
| prio | priority |
| pwm | pulse width modulation |
| q | queue |
| reg | register |
| rx | receive |
| sem | semaphore |
| str | string (null terminated) |
| sync | synchronize |
| temp | temperature |
| tmp | temporary |
| tx | transmit |
| usec | microsecond |

> ^1 Note that second(s) shall not be abbreviated, nor minute, hour, day, week, month, or year. Among other things, this rule eliminates conflict between minute and minimum (for “min”).

## Appendix B: Header File Template

```c
/** @file module.h
*
* @brief A description of the module's purpose.
*
* @par
* COPYRIGHT NOTICE: (c) 2018 Barr Group. All rights reserved.
*/

#ifndef MODULE_H
#define MODULE_H

int8_t max8(int8_t num1, int8_t num2);

#endif /* * MODULE_H */

*** end of file ***
```

## Appendix C: Source File Template

```c
/** @file module.c
 *
* @brief A description of the module's purpose.
 *
* @par
* COPYRIGHT NOTICE: (c) 2018 Barr Group. All rights reserved.
 */

#include <stdint.h>
#include <stdbool.h>

#include "module.h"

/*!
* @brief Identify the larger of two 8-bit integers.
* @param[in] num1 The first number to be compared.
* @param[in] num2 The second number to be compared.
* @return The value of the larger number.
 */
int8_t
max8 (int8_t num1, int8_t num2)
{
    return ((num1 > num2) ? num1 : num2);
}

/*** end of file ***/
```

## Appendix D: Example Program

```c
/** @file crc.h
 *
 * @brief Compact CRC library for embedded systems for CRC-CCITT, CRC-16, CRC-32.
 * @par
 * COPYRIGHT NOTICE: (c) 2000, 2018 Michael Barr. This software is placed in the
 * public domain and may be used for any purpose. However, this notice must not
 * be changed or removed. No warranty is expressed or implied by the
 * distribution of this source code.
 */

#ifndef CRC_H
#define CRC_H

// Compile-time selection of the desired CRC.
//
#if defined(CRC_CCITT)

#define CRC_NAME "CRC-CCITT"
uint16_t crc_t;

#elif defined(CRC_16)

#define CRC_NAME "CRC-16"
uint16_t crc_t;

#elif defined(CRC_32)

#define CRC_NAME "CRC-32"
uint32_t crc_t;

#else
#error "One of CRC_CCITT, CRC_16, or CRC_32 must be defined."
#endif

// Public API functions by the CRC library.
//
void crc_init(void);
crc_t crc_slow(uint8_t * const p_message, int n_bytes);
crc_t crc_fast(uint8_t * const p_message, int n_bytes);

#endif /* CRC_H */

*** end of file ***
```

```c
/** @file crc.c
*
* @brief Compact CRC generator for embedded systems, with brute force and table-
* driven options. Supports CRC-CCITT, CRC-16, and CRC-32.
*
 @par
* COPYRIGHT NOTICE: (c) 2000, 2018 Michael Barr. This software is placed in the
* public domain and may be used for any purpose. However, this notice must not
* be changed or removed. No warranty is expressed or implied by the
* distribution of this source code.
*/

#include <stdint.h>

#include "crc.h"

// Algorithmic parameters based on crc.h
//
#define BITS_PER_BYTE 8
#define WIDTH (BITS_PER_BYTE * sizeof(crc_t))
#define TOPBIT (1 << (WIDTH - 1))

// Allocate storage for the byte-wide CRC table.
//
#define CRC_TABLE_SIZE 256
static crc_t g_crc_table[CRC_TABLE_SIZE];

// Further configuration to support the selected CRC standard.
//
#if defined(CRC_CCITT)

#define POLYNOMIAL (uint16_t) 0x1021
#define INITIAL_REMAINDER (uint16_t) 0xFFFF
#define FINAL_XOR_VALUE (uint16_t) 0x0000
#define REFLECT_DATA(X) (X)
#define REFLECT_REMAINDER(X) (X)

#elif defined(CRC_16)

#define POLYNOMIAL (uint16_t) 0x8005
#define INITIAL_REMAINDER (uint16_t) 0x0000
#define FINAL_XOR_VALUE (uint16_t) 0x0000
#define REFLECT_DATA(X) ((uint16_t) reflect(X), BITS_PER_BYTE))
#define REFLECT_REMAINDER(X) ((uint16_t) reflect(X), WIDTH))

#elif defined(CRC_32)

#define POLYNOMIAL (uint32_t) 0x04C11DB7
#define INITIAL_REMAINDER (uint32_t) 0xFFFFFF
#define FINAL_XOR_VALUE (uint32_t) 0xFFFFFFFF
#define REFLECT_DATA(X) ((uint32_t) reflect(X), BITS_PER_BYTE))
#define REFLECT_REMAINDER(X) ((uint32_t) reflect(X), WIDTH))

#endif

/**
 * @brief Compute the reflection of a set of data bits around its center.
 * @param[in] data The data bits to be reflected.
 * @param[in] n_bits The number of bits.
 * @return The reflected data.
 */
static uint32_t
reflect(uint32_t data, uint8_t n_bits)
{
    uint32_t reflection = 0x00000000;

    // NOTE: For efficiency sake, n_bits is not verified to be <= 32.

    // Reflect the data about the center bit.
    //
    for (uint8_t bit = 0; bit < n_bits; ++bit)
    {
        // If the LSB bit is set, set the reflection of it.
        //
        if (data & 0x01)
        {
            reflection |= (1 << ((n_bits - 1) - bit));
        }

        data = (data >> 1);
    }

    return (reflection);
}

/* reflect() */

/**
 * @brief Initialize the lookup table for byte-by-byte CRC acceleration.
 *
 * @par
 * This function must be run before crc_fast() or the table stored in ROM.
 */
void
ncrc_init(void)
{
    // Compute the remainder of each possible dividend.
    //
    for (crc_t dividend = 0; dividend < CRC_TABLE_SIZE; ++dividend)
    {
        // Start with the dividend followed by zeros.
        //
        crc_t remainder = dividend << (WIDTH - BITS_PER_BYTE);

        // Perform modulo-2 division, a bit at a time.
        //
        for (int bit = BITS_PER_BYTE; bit > 0; --bit)
        {
            // Try to divide the current data bit.
            //
            if (remainder & TOPBIT)
            {
                remainder = (remainder << 1) ^ POLYNOMIAL;
            }
            else
            {
                remainder = (remainder << 1);
            }
        }

        // Store the result into the table.
        //
        g_crc_table[dividend] = remainder;
    }
}
```
