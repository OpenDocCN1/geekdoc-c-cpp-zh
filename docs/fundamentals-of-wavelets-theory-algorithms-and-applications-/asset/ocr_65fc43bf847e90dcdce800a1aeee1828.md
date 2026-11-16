structure, and signs of these encoded DWCs are also appended. This process is called the *dominant pass*.

+   - Those $C_{ij}$ encoded in previous higher thresholds are refined to a better accuracy by appending the bit corresponding to $T_k$. This process is called the *subordinate pass*.
+   - With decreasing thresholds, the leading zero bits of encoded DWCs are saved to achieve compression.
+   - The number of bits in the coded bit stream from a tree coder can be further reduced using a lossless entropy coder—for example, an arithmetic coder [12].

# 9.8.3 EZW Code

Initiated by Shapiro [14], the zerotree structure combined with bit plane coding is an efficient compression scheme for the discrete wavelet transformation. The *embedded zerotree wavelet* (EZW) coding scheme has proven its efficiency and flexibility in still image coding in terms of image quality and computation simplicity. Also, the EZW image coding algorithm generates an embedded bitstream in which information is sent to the decoder in the order of its importance; importance is judged by how much the information reduces the distortion of the reconstructed image. This embedded technique has two important advantages. First, the bit rate control allows one to stop the coding process at any point. Second, the image can be reconstructed from a point at which the encoded bitstream has been disrupted, even with reduced quality.

As an entropy coder, the zerotree coder takes advantage of the correlation between interleaved subbands of DWCs. Four symbols, $ZTR$, $POS$, $NEG$, and $IZ$, are used in the zerotree. A $ZTR$, zerotree root, represents a DWC and all of its descendants if they are insignificant, and it is the