understanding between-center effects.

proc plan can be utilized to generate the entire randomization scheme based on permuted block randomization. For example, in a two-arm trial, eight patients are enrolled for treatment assignment. With a block size of 4, there are six possible block patterns, i.e., $inom{4}{2}=6$. To invoke proc plan, we need to specify the number of blocks, the block size, and the number of treatments, as shown in Example Code 9.2 Permuted Block Randomization.

# Example Code 9.2 Permuted Block Randomization

```
proc plan seed=3;
factors Block=2 sequence=4 ordered / noprint;
treatments Treatment=4;
output out=PermutedBlock Treatment cvals=('A' 'A' 'B' 'B') random;
run;
```

```
proc sort data = PermutedBlock;
by block sequence;
run;
```

```
proc print data = PermutedBlock;
run;
```

The output for this permuted block design represents the treatment assignments of the eight patients. The result shows that the first block selected in the trial is block 2, and the first two patients in block 2 receive treatment B and the other two receive treatment A (Output for Example Code 9.2).

# Table 9.3 Output for Example Code 9.2

| Block | Sequence | Treatment |
|---|---|---|
| 1 | 1 | A |
| 1 | 2 | B |
| 1 | 3 | B |
| 1 | 4 | A |
| 2 | 1 | B |
| 2 | 2 | B |
| 2 | 3 | A |