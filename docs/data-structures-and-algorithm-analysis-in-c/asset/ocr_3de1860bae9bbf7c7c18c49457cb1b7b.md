array of length three. S0, S1, and S2 thus have four, four, and three suffixes, respectively. S0's suffixes are [ABR][ACA][DAB][RAS]. [ACA][DAB][RAS]. [DAB][RAS]. [RAS], which clearly correspond to the suffixes ABRACADABRA, ACADABRA, DABRA, and RA in the original string S. In the original string S, these suffixes are located at indices 0, 3, 6, and 9, respectively, so looking at all three of S0, S1, and S2, we can see that each S1 represents the suffixes that are located at indices i mod 3 in S.

Step 3: Concatenate S1 and S2 and recursively compute the suffix array. In order to compute this suffix array, we will need to sort the new alphabet of tri-characters. This can be done in linear time by three passes of radix sort, since the old characters were already sorted in step 1. If in fact all the tri-characters in the new alphabet are unique, then we do not even need to bother with a recursive call. Making three passes of radix sort takes linear time. If T(N) is the running time of the suffix array construction algorithm, then the recursive call takes T(2N/3) time.

# Example:

In our example

```
S1 S2 = [BRA], [CAD], [ABR], [A$$], [RAC], [ADA], [BRA]
```

The sorted suffixes that will be computed recursively will represent tri-character strings as shown in Figure 12.28.

Notice that these are not exactly the same as the corresponding suffixes in S; however, if we strip out characters starting at the first $, we do have a match of suffixes. Also note that the indices returned by the recursive call do not correspond directly to the indices in S, though it is a simple matter to map them back. So to see how the algorithm actually forms the recursive call, observe that three passes of radix sort will assign the following alphabet: [A$$] = 1, [ABR] = 2, [ADA] = 3, [BRA] = 4, [CAD] = 5, [RAC] = 6. Figure 12.29 shows the mapping of tri-characters, the resulting array that is formed for S1, S2, and the resulting suffix array that is computed recursively.

| Index | | Substring Being Represented |
|---|---|---|
| 0 | 3 | [A$$] [RAC] [ADA] [BRA] |
| 1 | 2 | [ABR] [A$$] [RAC] [ADA] [BRA] |
| 2 | 5 | [ADA] [BRA] |
| 3 | 6 | [BRA] |
| 4 | 0 | [BRA] [CAD] [ABR] [A$$] [RAC] [ADA] [BRA] |
| 5 | 1 | [CAD] [ABR] [A$$] [RAC] [ADA] [BRA] |
| 6 | 4 | [RAC] [ADA] [BRA] |

Figure 12.28 Suffix array for S1 S2 in tri-character set