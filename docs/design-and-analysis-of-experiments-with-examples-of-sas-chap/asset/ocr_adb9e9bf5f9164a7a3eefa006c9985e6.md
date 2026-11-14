# 9.4 Crossover Designs for Multiple Treatments

Many designs, with more than two treatments, have been proposed in the literature for crossover studies. Which design is best depends upon the assumptions made. For the two-treatment crossover design presented in the last section, only first-order carryover effects were assumed. That is to say, the treatment in a given period may affect the response in that period or the next period, but will not persist beyond that. Other more complicated models may assume second- or third-order carryover effects, or interactions between the carryover effect and the treatment given in the current period. These assumptions will result in more complicated designs. In this section designs will be described for the simple first-order carryover effects. For guidance on designs for more complicated models refer to Jones and Kenward (2003).

One desirable characteristic of a crossover design is variance balance where the variance of a difference in any pair of direct (or carryover) treatment effects is the same regardless of the pair. This balance can be achieved if every treatment is preceded by every treatment an equal number of times. For example, the simple AB, BA two-period crossover design is not balanced, because treatment A is only preceded by treatment B, and treatment B is only preceded by A. By adding the third period as in design 2, treatment A is preceded by B once and A once in the second sequence group, and treatment B is preceded by A once and B once in the first sequence group. Therefore design 2 is balanced.

# 9.4.1 Williams' Latin Square Crossover Designs

Balanced designs in t treatments and p = t periods can be created from Latin square designs. If there are no carryover effects, then a variance balanced design for direct treatment effects can be achieved by choosing any arbitrary t x t Latin square design. If carryover effects are possible, then variance balance can only be achieved when each treatment is preceded by every other treatment an equal number of times. Williams (1949) showed that this property could be achieved with only one particular Latin Square if t is an even number, and two particular Latin squares if t is an odd number. An easy algorithm for constructing these particular squares was described by Sheehe and Bross (1961) and is described below.

+   1. Number the treatments from 1 to t.

+   2. Start with a cyclic Latin square design where the treatments in the ith row are i, i + 1, ..., t, 1, ..., i - 1.

+   3. Create another latin square whose rows are the mirror images of the rows in the first Latin square; e.g., the mirror image of (1,2,3,4) is (4,3,2,1).

+   4. Interlace each row of the first Latin Square with the corresponding row of the second Latin square to produce a t x 2t rectangle. For example, interlacing (1, 2, 3, 4) with (4, 3, 2, 1) results in (1, 4, 2, 3, 3, 2, 4, 1).