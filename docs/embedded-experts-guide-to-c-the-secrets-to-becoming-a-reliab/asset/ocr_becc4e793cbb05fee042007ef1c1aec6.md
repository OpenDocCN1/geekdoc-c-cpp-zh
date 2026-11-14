```
error_bit |= parity (p_in[index + 1U] &
0x33U) << 1;
error_bit |= parity (p_in[index + 1U] &
0xFU) << 2;
b_half = p_in[index + 1U] ^
(0x80U >> error_bit);
b_half = (b_half & 0x7U) |
((b_half & 0x10U) >> 1);
/* Combines nibbles into one output
* byte. */
p_out[out_index] = (t_half << 4) | b_half;
++out_index;
}
}
```

Fig 6.4 - Hamming codes are easily computed error correcting codes; the most common is the Hamming (7,4) variant. Bit usage is more efficient than with basic repetition, but the total number of output bits is still almost twice the number of input bits. The encoding interleaves the three error checking bits with the four data bits in such a way as to produce a systematic code. This improves performance when decoding – the error-checking not only identifies if an error has occurred, but can also directly identify which bit has changed value. Furthermore, the example always “corrects” at least one-bit: since the Hamming codes are seven bits long, the most significant bit of the eight-bit bytes used can be changed without causing any problems. Other error correcting codes have been developed which are substantially more efficient, but also considerably more difficult to implement.