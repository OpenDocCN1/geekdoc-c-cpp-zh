```
/** @file crc.c
*
* @brief Compact CRC generator for embedded systems, with brute force and table-
* driven algorithm options. Supports CRC-CCITT, CRC-16, and CRC-32 standards.
*
* @par
* COPYRIGHT NOTICE: (c) 2000, 2018 Michael Barr. This software is placed in the
* public domain and may be used for any purpose. However, this notice must not
* be changed or removed. No warranty is expressed or implied by the publication
* or distribution of this source code.
*/

#include <stdint.h>

#include "crc.h"
```

```
// Algorithmic parameters based on CRC elections made in crc.h
//
#define BITS_PER_BYTE 8
#define WIDTH (BITS_PER_BYTE * sizeof(crc_t))
#define TOPBIT (1 << (WIDTH - 1))

// Allocate storage for the byte-wide CRC lookup table.
//
#define CRC_TABLE_SIZE 256
static crc_t g_crc_table[CRC_TABLE_SIZE];
```