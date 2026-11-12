# Considerations for running on other GPUs

Having now developed a program for a single, modern GPU, how well does i work on other GPUs? Often, especially if you are writing commercial applications, your program will need to work well on each level of hardware in the marketplace. Although programs will run on most GPU generations, you should be aware of what adaptations may be required to achieve good performance on that hardware. We’ll look at this with the AES program we’ve developed here.

Out first target is the GTX460 card, a compute 2.1 card based on Fermi. Major differences are the compute 2.1 architecture (7 SMs × 48 CUDA cores vs. 14 SMs × 32 CUDA cores), reduced L2 cache size (512 K vs. 640 K), reduced L1 cache size per CUDA core (48 KB L1 shared between 48 CUDA cores vs. 48K L1 shared among 32 CUDA cores), and the reduced memory bandwidth (115 GB/s vs. 134 GB/s).

Based purely on total CUDA core count (336 vs. 448), we’d expect around 75% of the performance. However, adjusting for clock speed differences, this gives us a little less than 10% performance difference between the two devices. Memory bandwidth is 15% less on the GTX460.

For the decrypt function the time actually measured is 100 ms compared with 61.5ms, which is somewhat disappointing. Looking at the execution profile we see that the SMS on the GTX460 are able to clock through more instructions, so the ratio of when the data arrives to the compute has changed. We again see a tiny amount of stalling in the SMS. With 128 threads per block we manage to get seven blocks scheduled (28 warps). If we could just reduce the register usage slightly we could execute another block and make better use of the SM. We therefore apply the same technique we used in the encode operation and move the inverse mix column operation closer to the decode operation. Thus,

```
// Add Round Key
//
// Fetch cipher key from memory as a 128 bit read
/*key_ptr = ((*cipher_key)[round_num]);
// Extract the key values, XOR’ing them with
// the current values
EXTRACT_WORD_XOR2((key_ptr->x), a0, a1, a2, a3);
EXTRACT_WORD_XOR2((key_ptr->y), a4, a5, a6, a7);
EXTRACT_WORD_XOR2((key_ptr->z), a8, a9, a10, a11);
EXTRACT_WORD_XOR2((key_ptr->w), a12, a13, a14, a15);
}
// Invert Column Mix on every round except the first
if (round_num != 10)
{
INV_MIX_COLUMN_PTR2(a0, a1, a2, a3,
gmul_14_ptr, gmul_09_ptr, gmul_13_ptr, gmul_11_ptr);
INV_MIX_COLUMN_PTR2(a4, a5, a6, a7,
gmul_14_ptr, gmul_09_ptr, gmul_13_ptr, gmul_11_ptr);
INV_MIX_COLUMN_PTR2(a8, a9, a10, a11,
gmul_14_ptr, gmul_09_ptr, gmul_13_ptr, gmul_11_ptr);
INV_MIX_COLUMN_PTR2(a12, a13, a14, a15,
```