
## CHAPTER 7. EVALUATION

| Program | static | dynamic | criterion |
|---|---|---|---|
| ptb_like | 65 173 | 49 124 | 9-8, 33-53 |
| mergesort | 123 299 | 97 216 | 45-14, 21-8 |
| cal | 240 648 | 0 0 | 228-10, 218-8 |
| | 134 315 | 44 92 | 367-12, 551-3 |
| agrep | 13170 40324 | 0 0 | 605-15, 638-7 |
| (sgrep.c) | 13138 40144 | 961 2345 | 96-14, 121-9 |
| patch | 16529 246754 | 6314 81365 | 825-23, 935-10 |

Table 7.5: Evaluation of static vs. dynamic chop sizes

the program agrep the criterion refer to the file agrep.c. they were chosen in a way to find conditions in the code which involve several variables that influence each other, preferably in loops. The goal was to produce interesting, path conditions. For example, the static chop in the program ptb_like (listed in Figure 7.13) from line 9 to line 33 ( ) contains 65 nodes connected by 173 edges. The dynamic chop, having 49 nodes and 124 edges. It is clear that the latter subgraph contains a noticeable smaller number of paths than the subgraph induced by the static chop. Sometimes the dynamic chop can rule out a dependence between two statements: Consider the first lines of the programs cal and agrep. One can see that dynamic chop for these criteria is empty. Following this evaluation of using traced value to improve precision in dynamic path conditions contains another example of that kind. In all these cases there was definitely no (illegal) information flow between the chopping criteria also static chop indicated.

After showing that chopping can considerably reduce the number of paths and yield a more precise path condition, which narrows the reasons for influence, we will present excerpts of path conditions and augment them with the restriction condition, which is based on trace data (using incomplete traces). Again, this information reveals variable values which may have contributed to the necessary condition that triggered an illegal information flow.

The first example ptb_like, shown in Figure 7.13, is taken from a weighing controller. Such a program represents the perfectly secure software we have in mind for this: There is part of the program, the so-calibrated buffer, which contains all paths from the sensor (p_ab) to the value display, in which the weight stored in u_kg (like 33). For a certificate that the machine is correctly calibrated one needs to ensure that there is no way to influence the calculation of the weight, for example by the keyboard. Consider the static path condition between the keyboard buffer p_cd in line 9 and the display of u_kg, which is the weight. The final path condition is shown in Figure 7.13. Note that this is bitwise logical and. An illegal information flow could only happen, if the keyboard buffer p_cd contained one of the special characters '+' or '-'. Since our runs use a keyboard buffer containing only ones, we expect the dynamic path condition to evaluate to false.

> It is actually original program to the Java version in Figure 7.8

```
#define TRUE 1
#define CTRL2 0
#define PB 0
#define PA 1
void printf();
void main() {
{
    int p_ab[2] = {0, 1};
    int p_cd[2] = {1, 1};
    char e_puf[8] = =
        {'0','0','0','0','0','0','0','0'};
    int u = 0;
    int idx = 0;
    float u_kg = 0.0;
    float kal_kg = 1.0;

    while (TRUE) {
        if ((p_ab[CTRL2] & 0x10)==0) {
            u = ((p_ab[PB] << 8) +
                (unsigned int)e_puf[PA]);
            u_kg = (float)u * kal_kg;
        }
        if ((p_cd[CTRL2] & 0x01) != 0) {
            for (idx=0; idx<7; idx++) {
                e_puf[idx] = (char)p_cd[PA];
                if (p_cd[CTRL2] & 0x10) != 0) {
                    e_puf[idx] = 'a';
                    kal_kg = 1.01; /* illegal */
                } else if (e_puf[idx] == '-') {
                    kal_kg = 0.99; /* illegal */
                }
            }
        }
        e_puf[idx] = '\0';
    }
    printf("Article:%7.7s\n" +
        ""%6.2fkg%%%%",e_puf,u_kg);
}
n}
```

Figure 7.13: ptb_like

```
1 ( ((p_cd[0] & 0x01) != 0)
2 ^ ((p_cd[0] & 0x10) != 0)
3 ^ ((p_ab[0] & 0x10) == 0)
4 ^ (e_puf[idx] == '\'+')
5 ^ (idx < 7) )
6 V
7 ( ((p_cd[0] & 0x01) != 0)
8 ^ ((p_cd[0] & 0x10) != 0)
9 ^ (e_puf[idx] == '\'-')
10 ^ ((p_ab[0] & 0x10) == 0)
11 ^ (e_puf[idx] != '\'+')
12 ^ (idx < 7) )
```

Figure 7.14: Static patch condition for ptb_like

```
1 .. , V
2 ( e_puf == <unknown>
3 ^ idx == 0
4 ^ p_cd == {1, 1}
5 ^ p_ab == {0, 1}
6 ^ ((p_cd[0] & 0x01) != 0)
7 ^ ((p_cd[0] & 0x10) != 0)
8 ^ (e_puf[idx] == '\'-')
9 ^ ((p_ab[0] & 0x10) == 0)
10 ^ (e_puf[idx] != '\'+')
11 ^ (idx < 7) )
12 V . . .
```

Figure 7.15: Excerpt of a dynamic patch condition for ptb_like

```
1 ((p_cd[0] & 0x1) != 0)
2 ^ ((p_cd[0] & 0x10) != 0)
3 ^ ((p_ab[0] & 0x10) == 0)
4 ^ (e_puf[idx] == '+')
5 ^ (idx < 7)
```

Figure 7.16: Dynamic path condition of illegal flow in ptb_like

Using a dynamic chop immediately reveals that: the static path condition describes a path that was not taken during runtime, the precise dynamic path condition yields false. The dynamic path condition based on the static chop, in contrast, consists of ten conjunctive blocks, one of which is shown in Figure 7.15. Dynamic trace is shown in bold, e_puf has not been traced (incomplete trace). As one can see, the particular predicates

p_cd == <1, 1>

and

((p_cd[0] & 0x10) != 0)

contradict each other, so that the given block evaluates to false. The same goes with the other blocks and we expect the result false. The path condition cannot be fulfilled; the necessary path was not taken. This proves that the keyboard buffer had no influence on the output presented to the consumer. In another scenario, the input p_cd = (0xff, '+') (instead of line 9) has been traced. Upon entering '+' on the keyboard, the displayed value is too high. With the dynamic path condition detection of the illicit influence becomes automatically: Figure 7.16 shows the path condition for the adapted program based on the dynamic rather than the static chop. The traced input can exactly determine where the illicit information flow took place. Together with the definition of e_puf, the restrictive condition yields:

```
1 (p_cd[0] == 0)
2 ^ (p_ab[0] == 0)
3 ^ (p_cd[0] == '+')
4 ^ (idx < 7)
```

This path condition shows why there was an illegal information flow during program execution producing incorrect output (the weight on the machine): The display was influenced by some debug flags and the input of '+' during the 7 rounds of the for-loop The programmers happily forgotten to remove the debugging code from the final version. This information can act as a witness to reproduce the illicit behavior. In this small example one can see that the calibration u_kg is increased in line 26 by such an input. For larger examples a human would most probably not detect illegal statements so easily.

As another example, consider the mergesort from Figure 7.19. Figure 7.17 shows the statically computed path condition between 999 in line 45

## CHAPTER 7. EVALUATION

```
1 (left < right)
2 ^ (idx1 <= ((left + right) / 2))
3 ^ (data[idx1] >= data[idx2])
4 ^ (idx2 <= right)
```

Figure 17: Static path condition for mergesort

```
1 right == 4
2 ^ left == 4
3 ^ data == 1
4 ^ idx2 == 5
5 ^ ((left + right) / 2) == 3
6 ^ idx1 == 3
7 ^ (left < right)
8 ^ (idx1 <= ((left + right) / 2))
9 ^ (data[idx1] >= data[idx2])
10 ^ (idx2 <= right)
```

Figure 18: Excerpt of a dynamic path condition for mergesort

and temp in line 21. This time, using a dynamic chop does not strengthening the path condition as the dynamic chop is identical to the static path condition regarding the paths relevant to the path condition. however, yields 40 conjunctive blocks, one of which is shown in Figure 7.18. Dynamic trace data is again shown below. Due to contradictions within the particular blocks, the condition can be fully evaluated to false: there was no program state trace would have fulfilled the static path condition.

As our examples show, dynamic path conditions are usually a good deal better than their computed counterparts, but also more precise as they hold more information. Each dynamic path condition is tied to a particular program run. If a dynamic path condition evaluates to false does not necessarily hold for each program execution, unless input is involved. But dynamic path conditions are a means of finding witnesses for illegal behavior.

### Omission errors

Dynamic slices can show that some influence took place or not. Sometimes one would like to know why an expected influence did not happen during program execution. In literature [AHKL93, GABF99, WR04] several approaches were proposed to enrich the dynamic slice with the "culpable" control predicates, i.e. those that triggered a branch to an execution on which the expected data dependence did not come into effect. But adding the predicates to the slice does not reveal what actually went wrong. Our approach returns the exact conditions for a data flow to happen. The static path condition augmented with the restrictive clause can be fed into a constraint solver to detect the contradictions between the variable trace and the values
