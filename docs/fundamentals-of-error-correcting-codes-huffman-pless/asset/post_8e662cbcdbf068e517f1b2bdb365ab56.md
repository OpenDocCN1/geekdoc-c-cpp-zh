
| c_{1,1} | c_{2,1} | c_{3,1} | c_{4,1} | c_{5,1} | c_{6,1} | c_{7,1} | c_{8,1} | c_{9,1} | c_{10,1} | c_{11,1} | c_{12,1} | c_{13,1} | ... |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | c_{1,2} | c_{2,2} | c_{3,2} | c_{4,2} | c_{5,2} | c_{6,2} | c_{7,2} | c_{8,2} | c_{9,2} | ... |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | c_{1,3} | c_{2,3} | c_{3,3} | c_{4,3} | c_{5,3} | ... |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | c_{1,4} | ... |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

Figure 5.2 4-frame delay interleaving.

This separates samples as far apart as possible within the new frame. These permutations of bytes allow for error concealment as we discuss later. This 24-byte message consisting of a vector in \(\mathbb{F}_{256}^{24}\) is encoded using a systematic encoder for a [28, 24, 5] shortened Reed-Solomon code, which we denote \(C_1\). This code produces four bytes of redundancy, that is, two pairs \(P_1\) and \(P_2\) each with two bytes of parity which are then placed in the middle of all above to form

\(L_1 L_3 L_5 R_1 R_3 R_5 P_1 P_2 \tilde{L}_2 \tilde{L}_4 \tilde{L}_6 \tilde{R}_2 \tilde{R}_4 \tilde{R}_6 \tilde{R}_8\).

further separating the odd-numbered samples from the even-numbered samples.

Thus from \(C_1\) we produce a string of 28-byte codewords which we interleave to a depth of 28 using 4-frame delay interleaving as we now describe. Begin with codewords \(\mathbf{c}_1, \mathbf{c}_2, \dots\) from \(C_1\) in the order they are generated. Form an array with 28 rows and a large number of columns in the following fashion. Row 1 consists of the first byte of \(\mathbf{c}_1\) in column 1, the first byte of \(\mathbf{c}_2\) in column 2, the first byte of \(\mathbf{c}_3\) in column 3, etc. Row 2 begins with four bytes equal to 0 followed by the second byte of \(\mathbf{c}_1\) in column 5, the second byte of \(\mathbf{c}_2\) in column 6, the second byte of \(\mathbf{c}_3\) in column 7, etc. Row 3 begins with eight bytes equal to 0 followed by the third byte of \(\mathbf{c}_1\) in column 9, the third byte of \(\mathbf{c}_2\) in column 10, the third byte of \(\mathbf{c}_3\) in column 11, etc. Continue in this manner filling out all 28 rows. If \(\mathbf{c}_i = c_{i,1} c_{i,2} \cdots c_{i,28}\), the resulting array begins as in Figure 5.2, and thus the original codewords are found going diagonally down this array with slope -1/4. This array will be as long as necessary to accommodate all the encoded frames of data. All the rows except row 28 will need to be padded with zeros so that the array is rectangular; see Exercise 323.

### Exercise 323 Suppose a CD is used to record 72 minutes of sound. How many frames of data does this represent? How long is the array obtained by interleaving the codewords in \(C_1\) corresponding to all these frames to a depth of 28 using 4-frame delay interleaving?

## Step II: Encoding using \(C_2\) and interleaving

Each column of the array is a vector in \(\mathbb{F}_{256}^{28}\) which is then encoded using a [32, 28, 5] shortened Reed-Solomon code \(C_2\). Thus we now have a list of codewords, which are generated in the order of the columns, each consisting of 32 bytes. The codewords are regrouped with the odd-numbered symbols of one codeword grouped with the even-numbered symbols of the next codeword. This regrouping is another form of interleaving which further breaks up short bursts that may still be present after the 4-frame delay interleaving. The regrouped bytes are written consecutively in one long stream. We now re-divide this long string into segments of 32 bytes, with 16 bytes from one C2 codeword and 16 bytes from another C2 codeword because of the above regrouping. At the end of each of these segments a 33rd byte is added which contains control and display information. Thus each frame of six samples eventually leads to 33 bytes of data. A schematic of the encoding using C1 and C2 can be found in [154].

## Step III: Imprinting and EFM

Each byte of data must now be imprinted onto the disc. First, the bytes are converted to strings of bits using EFM described shortly. Each bit is of length 0.3 μm when imprinted along the track. Each land-to-pit or pit-to-land transition is imprinted with a single 1, while the track along the pit or land is imprinted with a string of 0s whose number corresponds to the length of the pit or land. For example, a pit of length 2.1 μm followed by a land of length 1.2 μm corresponds to the string 100000001000. For technical reasons each land or pit must be between 0.9 and 3.3 μm in length. Therefore each pair of 1s is separated by at least two 0s and at most ten 0s. Thus the 256 possible bytes must be converted to bit strings in such a way that this criterion is satisfied. Were it not for this condition, one could convert the bytes to elements of \(\mathbb{F}_2^8\), it turns out that the smallest string length such that there are at least 256 different strings where each 1 is separated by at least two 0s but no more than ten 0s is length 14. In fact there are 267 binary strings of length 14 satisfying this condition; 11 of these are not used. This conversion from bytes to strings of length 14 is called EFM or eight-to-fourteen modulation. Note, however, that bytes must be encoded in succession, and so two consecutive 14-bit strings may fail to satisfy our conditions on minimum and maximum numbers of 0s between 1s. For example 10010000000100 and 0000000010001 are both allowable strings but if they follow one after the other, we obtain

```
1001000000010000000000010001,
```

which has 11 consecutive 0s. To overcome this problem three additional bits called merge bits are added to the end of each 14-bit string. In our example, if we add 001 to the end of the first string, we have

```
100100000001000010000000010001,
```

which satisfies our criterion. So our frame of six samples leads to 33 bits each of which is converted to 17 bits. Finally, at the end of these 33 · 17 bits, 24 synchronization bits plus three merging bits are added; thus each frame of six samples leads to 588 bits.

### Exercise 324 Do the following; see the related Exercise 323:

- (a) How many bits are on the track of a CD with 72 minutes of sound?
- (b) How long must the track be if each bit is 0.3 μm in length?

1 The control and display bytes include information for the listener such as playing time, composer, and title of the piece, as well as technical information required by the CD player.

## 5.6.2 Decoding

We are now ready to see how decoding and error-correction is performed by the CD player.² The process reverses the encoding.

Step 1: Decoding with C2 First, the synchronization bits, control and display bits, and merging bits are removed. Then the remaining binary strings are converted from EFM form into byte form, a process called demodulation, using table look-up; we now have our data as a stream of bytes. Next we undo the scrambling done in the encoding process. The stream is divided into segments of 32 bytes. Each of these 32-byte segments contains odd-numbered bytes from one codeword (with possible errors, of course) and even-numbered bytes from the next. The bytes in the segments are regrouped to restore the positions in order and are passed on to the decoder for C2. Note that if a short burst error had occurred on the disc, the burst may be split up into shorter bursts by the regrouping. As C2 is a [32, 28, 5] code over \(\mathbb{F}_{256}\), it can correct two errors. However, it is only used to correct single errors or detect the presence of multiple errors, including all errors of size two or three and some of larger size. The sphere of radius 1 centered at some codeword \(c_1\) does not contain a vector that differs from another codeword \(c_2\) in at most three positions as \(c_1\) and \(c_2\) are distance at least five from one another. Therefore, if a single error has occurred, C2 can correct that error; if two or three errors have occurred, C2 can detect the presence of those errors (but will not be used to correct them).

What is the probability that C2 will fail to detect four or more errors when we use C2 to correct only single errors? Such a situation would arise if errors are made in one codeword so that the resulting vector lies in a sphere of radius 1 about another codeword. Assuming all vectors are equally likely, the probability of this occurring is approximately the ratio of the total number of vectors inside spheres of radius 1 centered at codewords to the total number of vectors in \(\mathbb{F}_{256}^{32}\). This ratio is

\frac{256^{28}(1 + 32(256 - 1))}{256^{32}} = \frac{8161}{256^4} \approx 1.9 \times 10^{-6}.

By Exercise 325, if C2 were used to its full error-correcting capability by correcting all double errors, then the probability that three or more errors would go undetected is about \(7.5 \times 10^{-3}\). The difference in these probabilities indicates why the full error-correcting capability of C2 is not used since the likelihood of three or more errors going undetected (or being miscorrected) is much higher with full error-correction.

### Exercise 325 Verify the following:

- (a) A sphere of radius 2 centered at a codeword of a [32, 28] code over \(\mathbb{F}_{256}\) contains

1 + 32(256 - 1) + \binom{32}{2}(256 - 1)^2

vectors in \(\mathbb{F}_{256}^{32}\).

2 The encoding of a digital video disc (DVD) involves Reed-Solomon codes in a fashion similar to the CD. Tom Høholdt has created a simulation of DVD decoding at the following web site: http://www.mat.dtu.dk/persons/hoeholdt/Tom/.
