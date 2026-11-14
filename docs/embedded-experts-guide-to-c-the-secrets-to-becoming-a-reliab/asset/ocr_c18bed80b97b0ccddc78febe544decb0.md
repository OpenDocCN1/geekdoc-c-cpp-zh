```
}
else if (2U == in_size)
{
/* Two input bytes are left – encode
* them. */
index[0] = p_in[0] >> 2;
index[1] = ((p_in[0] & 0x3U) << 4) |
(p_in[1] >> 4);
index[2] = ((p_in[1] & 0xFU) << 2);
p_out[0] = b64_table[index[0]];
p_out[1] = b64_table[index[1]];
p_out[2] = b64_table[index[2]];
out_size += 3U;
}
else
{
/* All input bytes have been encoded. */
}
/* Return the size of the output. */
return out_size;
}
```

Fig 6.1 - Encoding of data to Base64 can be achieved by using a lookup table to find the corresponding character for each six bits of the original data. Every three bytes of input produce four bytes of output. Several improvements could be made to this example – but it has been made deliberately verbose to better illustrate the methods being used. The output does not include any padding bytes in the output – although not required for accurate decoding of the output, these are sometimes added to the output until the total length is a multiple of four bytes in length. The character (ASCII code 61) is commonly used. Decoding can be achieved