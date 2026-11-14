
## 8.15.1.3 Response

When data is corrupted, one can detect the damaged bits and signal that an error has occurred, or one can detect and then correct the problem (depending on the extent of the error). However, the cost (time and added bits) of the correction algorithm must be considered.

## 8.15.2 Managing Damaged Data

Several alternatives exist for dealing with data that has been corrupted. The choices are simple: ignore it, detect it, or detect and correct it. For either of the last two alternatives, additional information must be incorporated into the data object. The amount of additional information that is needed depends on the kinds of faults to be detected and the intended response.

## 8.15.2.1 Parity

- odd parity The simplest form of detection is called parity. The basic scheme appends a single bit to each data word or block. When using odd parity, the total number of one bits (including the parity bit) must be odd. If the data word has an odd number of one bits, a 0 is added; if the data word has an even number of one bits, a 1 is added.

- even parity For even parity, the total number of one bits (including the parity bit) must be even. If the data word has an odd number of one bits, a 1 is added; if the data word has an even number of one bits, a 0 is added. Before the data is used, the parity is recomputed and compared with the expected. A mismatch indicates an error. If there is no mismatch, the best that can be said is that either no errors have occurred or an even number of errors have occurred.

The advantage of such a scheme is that it is simple and detects all odd numbers of errors. The simplicity of the approach, however, also gives rise to several problems. The approach does not work reliably for burst errors and, also, it is a "detection only" scheme.

The basic parity codes have a Hamming distance of two. That is, 2-bit changes are required before one valid data word is changed into another.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_421_0.png)

Three-bit words are used in Figure 8.18 to illustrate how to compute and check the parity bit for each of the schemes.

When checking for errors in this example, only single-bit errors are assumed to have occurred.

## 8.15.2.2 Linear Codes

Implementing data error detection using the basic parity scheme is sufficient for many applications. If greater detection as well as correction capabilities are necessary, then a more sophisticated approach is appropriate. A good first step toward adding greater capabilities to a fault management scheme utilizes an encoding scheme that generates a family of codes called linear codes. Such codes are designated linear because the arithmetic combination of two existing words gives a third word that is also in the set of valid code words.

- linear codes Such codes are designated linear because the arithmetic combination of two existing words gives a third word that is also in the set of valid code words.

- encoding The term encoding in the current context refers to the process of adding parity bits to the data word to provide enhanced detection and correction capabilities. Code, code word, or encoded word specifies the data word with the additional parity bits.

- Hamming codes The first types of linear codes that we will look at are called the Hamming codes.

| Original Data | Odd Data Parity | Even Data Parity |
|---|---|---|
| 000 | 000 1 | 000 0 |
| 001 | 001 0 | 001 1 |
| 010 | 010 0 | 010 1 |
| 011 | 011 1 | 011 0 |
| 100 | 100 0 | 100 1 |
| 101 | 101 1 | 101 0 |
| 110 | 110 1 | 110 0 |
| 111 | 111 0 | 111 1 |

| Data Received | Odd Parity Result | Even Parity Result |
|---|---|---|
| 0000 | Error | Valid |
| 0001 | Valid | Error |
| 0010 | Valid | Error |
| 0011 | Error | Valid |
| 0100 | Valid | Error |
| 0101 | Error | Valid |
| 0110 | Error | Valid |
| 0111 | Valid | Error |
| 1000 | Valid | Error |
| 1001 | Error | Valid |
| 1010 | Error | Valid |
| 1011 | Valid | Error |
| 1100 | Error | Valid |
| 1101 | Valid | Error |
| 1110 | Valid | Error |
| 1111 | Error | Valid |

Figure 8.18 Generating and Checking Parity for a 3-bit Data Word.

## 8.15.2.2.1 HAMMING CODES

A strategy developed by Hamming demonstrated a method for encoding data words with a minimum distance of three. Following encoding, data could be transmitted with the assurance that on reception, any single-bit error could be corrected and any double-bit error could be detected.

To execute the encoding process, one must specify the number of data bits and the number of parity bits. These two are related as follows.

```
Encoded word length = 2^p – 1
Number of parity bits = p
Number of data bits = 2^p – p – 1
```

The approach requires that the parity bits be inserted into the data field in a particular way. Starting with the first bit position, any position that is a power of two should contain a parity bit; all remaining positions are used to store data bits. Thus, positions 1, 2, 4, 8, ... will hold parity bits. The approach also specifies the bits over which each of the parity bits computes parity. The assignment works as follows.

Numbering begins with the least significant bit, which is labeled bit 1.

- 1. Parity bits are placed in bit positions: 1, 2, 4, 8, 16 ... Data bits are placed in the other positions.
- 2. The parity bits are chosen such that they provide even parity over the following groups of bit positions:

| a. | P0: 1, 3, 5, 7, ... | P0 will be in position 1 |
|---|---|---|
| b. | P1: 2, 3, 6, 7, 10, 11, ... | P1 will be in position 2 |
| c. | P2: 4, 5, 6, 7, 12, 13, 14, 15 ... | P2 will be in position 4 |

The encoded word appears as in Figure 8.19.

| 7 | 6 | 5 | 4 | 3 | 2 | 1 |
|---|---|---|---|---|---|---|
| D3 | D2 | D1 | P2 | D0 | P1 | P0 |

**Figure 8.19** Hamming Encoding Scheme for a 4-bit Data Word.

Upon reception, the parity bits are recomputed. If the recomputed set of parity bits is all zero, the received word contained no errors; otherwise, the binary value of the bits in the recomputed set identifies the bit that is in error. At that point, the designated bit can simply be inverted.

The data word is illustrated in Figure 8.20.

| 4 | 3 | 2 | 1 |
|---|---|---|---|
| 1 | 1 | 0 | 1 |

**Figure 8.20** Sample Data Word.

The encoding is given as in Figure 8.21.

| 7 | 6 | 5 | 4 | 3 | 2 | 1 |
|---|---|---|---|---|---|---|
| 1 | 1 | 0 | 0 | 1 | 1 | 0 |

**Figure 8.21** The Data Word is Encoded.

Assume that the encoded word shown in Figure 8.22 is received.

| 7 | 6 | 5 | 4 | 3 | 2 | 1 |
|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 0 | 1 | 1 | 0 |

**Figure 8.22** Corrupted Received Data Word.

Each of the parity bits is computed as:

- P0: {1, 3, 5, 7} parity is 0
- P1: {2, 3, 6, 7} parity is 1
- P2: {4, 5, 6, 7} parity is 1.

The check is showing a value of 110, binary 6. Indeed, bit 6 is the one that is incorrect. Had the check number been 0, the received word would have been correct.

## 8.15.2.2.2 BLOCK CODES

- block codes
- block check codes
- block check sum

Block codes are the subset of linear codes in which error management is performed over blocks of data words rather than individual words. Among the simpler implementations of such codes are the block check codes. Encoding data using such codes begins with computing parity for each individual word as we did earlier. Next, a group of words is aggregated into a block or frame, and a parity word called a block check sum is computed over the entire block. The block check sum is a simple extension of the single parity bit idea, and it applies to a complete block or frame of data. The block check sum is computed according to the following rules.

- 1. The parity of each individual word is computed as in the base case; the parity bit is now referred to as a “lateral” or “row” parity bit.
- 2. A parity word is computed for the block as follows.
- Bit 0 – Parity of bit 0 of all words in the block
- Bit 1 – Parity of bit 1 of all words in the block
- Bit n – Parity of all lateral parity bits in the block.

This word is called “longitudinal” or “column” parity.

Figure 8.23 schematically illustrates a block of data (made up of 4-bit words) and the two parity check bits for the data block.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_424_0.png)

Figure 8.23 Computing Lateral and Longitudinal Parity in a Block Check Scheme.
