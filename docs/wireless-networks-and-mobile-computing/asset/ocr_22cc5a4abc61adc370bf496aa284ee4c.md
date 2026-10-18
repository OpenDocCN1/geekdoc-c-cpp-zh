of the design by Sen Gupta et al. [1]. Detailed comparative results are presented in Table 9.4; Design 1 refers to the design approach described in Section 9.3.

**TABLE 9.4:** Timing comparison of Design 1 with those of [11], [17] and [18].

| Operations | [11] and [17] | [18] | Design 1 |
|---|---:|---:|---:|
| Per KSA round | 3 | 1 | 1 |
| Complete KSA | 256 × 3 = 768 | 256 + 3 = 259 | 256 + 1 = 257 |
| *N* bytes of PRGA | *N* + 3 | *N* + 3 | *N* + 2 |
| *N* bytes of RC4 | 3*N* + 768 | 259 + (*N* + 3) = *N* + 262 | 257 + (*N* + 2) = *N* + 259 |
| Cycles per byte | 3 + 768/*N* | 1 + 262/*N* | 1 + 259/*N* |

The obvious advantage of the design proposed in [18] is its compactness. However, the documentation does not report area or timing figures corresponding to any technology node. Instead, a figurative summary of the logic structure is reported. Also in [18], neither the hardware implementation of KSA nor the port access sharing between PRGA and KSA is reported.

# 9.3.5 Yet Another Design Approach for RC4

This section presents a pipelined design approach for RC4 generation as proposed by Sen Gupta et al. [1].

**Pipelined Design A:** This design approach is based on an architecture pipelined in two stages, as in Figure 9.9. While [18] proposed a deep pipelining with bypass and data-forwarding, this scheme allows a simpler two-stage pipelining with the same throughput of 1 byte per cycle and similar memory port restrictions. The first pipeline stage is devoted to calculation of *j* and performing the swap and the second pipeline stage computes the value of *Z*. To minimize the read and write accesses to *S*-box, the index to be used for second pipeline is computed at the first stage. Note that the index computation at first stage does not alter the result as *S[i]* and *S[j]* are swapped; thus the addition result *S[i] + S[j]* remains intact.

With the aforementioned structure, the pipeline in the PRGA circuit is consid-