```
a10 = tmp10;
a11 = tmp11;
a12 = tmp12;
a13 = tmp13;
a14 = tmp14;
a15 = tmp15;
}
```

The next step is to mix the columns operation, which is done in every round except the last one. The previous mix column code shown earlier had the c loop unrolled to form the MIX_COL macro. Additionally, to control the order of the XOR, we implement an XOR_5, which is a five-input XOR macro.

```
// Addkey
a0 ^= EXTRACT_D0(w0);
a4 ^= EXTRACT_D1(w0);
a8 ^= EXTRACT_D2(w0);
a12 ^= EXTRACT_D3(w0);
a1 ^= EXTRACT_D0(w1);
a5 ^= EXTRACT_D1(w1);
a9 ^= EXTRACT_D2(w1);
a13 ^= EXTRACT_D3(w1);
a2 ^= EXTRACT_D0(w2);
a6 ^= EXTRACT_D1(w2);
a10 ^= EXTRACT_D2(w2);
a14 ^= EXTRACT_D3(w2);
a3 ^= EXTRACT_D0(w3);
a7 ^= EXTRACT_D1(w3);
a11 ^= EXTRACT_D2(w3);
a15 ^= EXTRACT_D3(w3);
round_num++;
}
```

We then implement the XOR operation with the key fetched at the start of the loop.

```
cipher_block->w = (ENCODE_D0(a0) | ENCODE_D1(a4) | ENCODE_D2(a8) | ENCODE_D3(a12));
cipher_block->x = (ENCODE_D0(a1) | ENCODE_D1(a5) | ENCODE_D2(a9) | ENCODE_D3(a13));
cipher_block->y = (ENCODE_D0(a2) | ENCODE_D1(a6) | ENCODE_D2(a10) | ENCODE_D3(a14));
cipher_block->z = (ENCODE_D0(a3) | ENCODE_D1(a7) | ENCODE_D2(a11) | ENCODE_D3(a15));
}
```

Finally, the resultant key is combined into a 32-bit value and written back to the uint4 cipher word. At this point we've completed all 10 rounds and the cipher block is encoded based on the set of 10 round keys.

For completeness purposes, the macros used are defined as follows:

```
#define EXTRACT_D0(x) ( ( (x) >> 24ul ) )
#define EXTRACT_D1(x) ( ( (x) >> 16ul ) & 0xFFuL )
```