
- Resolution ≥ 5 means there is no confounding between main effects, between two-factor interactions, or between main effects and two-factor interactions.

All the fractional factorial designs are *minimum aberration* designs. For DOE experts, the minimum aberration design of a given resolution minimizes the number of words in the defining relation that are of minimum length.

The figure on the right in Figure 12.8 is geometric representation of a two-level fractional factorial design.

## Figure 12.8 Representation of Full Factorial (Left) and Two-Level Fractional Factorial (Right) Designs

![](img/a858f3b35ed4923af65c22e8829ee5a8_205_0.png)

## Plackett-Burman Designs

Plackett-Burman designs are an alternative to fractional factorials for screening. One useful characteristic is that the sample size is a multiple of four rather than a power of two. There are no two-level fractional factorial designs with sample sizes between 16 and 32 runs. However, there are 20-run, 24-run, and 28-run Plackett-Burman designs.

The main effects are orthogonal and two-factor interactions are only partially confounded with main effects. This is different from resolution-three fractional factorial where two-factor interactions are indistinguishable from main effects.

In cases of effect sparsity, a stepwise regression approach can allow for removing some insignificant main effects while adding highly significant and only somewhat correlated two-factor interactions.

## Mixed-Level Designs

If you have qualitative factors with three values, then none of the classical designs discussed previously are appropriate. For pure three-level factorials, JMP offers fractional factorials. For mixed two-level and three-level designs, JMP offers complete factorials and specialized orthogonal-array designs, listed below.

## Table 12.1

| Design | Two-Level Factors | Three-Level Factors |
|---|---|---|
| L18 John | 1 | 7 |
| L18 Chakravarty | 3 | 6 |
| L18 Hunter | 8 | 4 |
| L36 | 11 | 12 |

If you have fewer than or equal to the number of factors for a design listed in the table, you can use that design by selecting an appropriate subset of columns from the original design. Some of these designs are not balanced, even though they are all orthogonal.

## Cotter Designs

Cotter designs are used when you have very few resources and many factors, and you believe there may be interactions. Suppose you believe in effect sparsity— that very few effects are truly nonzero. You believe in this so strongly that you are willing to bet that if you add up a number of effects, the sum will show an effect if it contains an active effect. The danger is that several active effects with mixed signs will cancel and still sum to near zero and give a false negative.

Cotter designs are easy to set up. For k factors, there are 2k + 2 runs. The design is similar to the “vary one factor at a time” approach many books call inefficient and naive.

A Cotter design begins with a run having all factors at their high level. Then follow k runs each with one factor in turn at its low level, and the others high. The next run sets all factors at their low level and sequences through k more runs with one factor high and the rest low. This completes the Cotter design, subject to randomizing the runs.

When you use JMP to generate a Cotter design, JMP also includes a set of extra columns to use as regressors. These are of the form factorOdd and factorEven where factor is a factor name. They are constructed by adding up all the odd and even interaction terms for each factor. For example, if you have three factors, A, B, and C:

## Figure 12.9

AOdd = A + ABC      AEven = AB + AC
BOdd = B + ABC      BEven = AB + BC
COdd = C + ABC      CEven = BC + AC

Because these columns in a Cotter design make an orthogonal transformation, testing the parameters on these combinations is equivalent to testing the combinations on the original effects. In the example of factors listed above, AOdd estimates the sum of odd terms involving A. AEven estimates the sum of the even terms involving A, and so forth.

Because Cotter designs have a false-negative risk, many statisticians discourage their use.

## How to Run a Cotter Design

By default, JMP does not include a Cotter design in the list of available screening designs (Figure 12.7). However, if you would like to make a Cotter design:

- 1. Immediately after entering responses and factors (and before clicking Continue), click the red triangle icon in the Screening Design title bar.
- 2. Select Supress Cotter Designs.

Changing the setting via the red triangle menu applies only to the current design. To alter the setting for all screening designs:

- 1. Select File > Preferences.
- 2. Click the Platform icon.
- 3. Click DOE to highlight it.
- 4. Uncheck the box beside Supress Cotter Designs.

## Figure 12.14 The Third Level Alias for the Five-Factor Reactor Example

![](img/a858f3b35ed4923af65c22e8829ee5a8_209_0.png)

## Understanding the Coded Design

In the coded design panel, each row represents a run. Plus signs designate high levels and minus signs represent low levels. As shown in Figure 12.15, rows for the first three columns of the coded design, which represent Feed Rate, Catalyst, and Stir Rate are all combinations of high and low values (a full factorial design). The fourth column (Temperature) of the coded design is the element-by-element product of the first three columns. Similarly, the last column (Concentration) is the product of the second and third columns.

## Figure 12.15 Default Coded Designs

![](img/a858f3b35ed4923af65c22e8829ee5a8_209_1.png)

## Changing the Coded Design

In the Change Generating Rules panel, changing the checkmarks and clicking Apply changes the coded design; it changes the choice of different fractional factorial designs for a given number of factors. The Change Generating Rules table in Figure 12.16 shows how the last two columns are constructed in terms of the first three columns. The check marks for Temperature show it is a function of Feed Rate, Catalyst, and Stir Rate. The checkmarks for Concentration show it is a function of Catalyst and Stir Rate.

If you check the options as shown in Figure 12.16 and click Apply, the Coded Design panel changes. The first three columns of the coded design remain a full factorial for the first three factors (Feed Rate, Catalyst, and Stir Rate). Temperature is now the product of Feed Rate and Catalyst, so the fourth column of the coded design is the element by element product of the first two columns. Concentration is a function of Feed Rate and Stir Rate.

## Figure 12.16 Modified Coded Designs and Generating Rules

![](img/a858f3b35ed4923af65c22e8829ee5a8_210_0.png)

## Specifying Output Options

Use the Output Options panel to specify how you want the output data table to appear. When the options are correctly set up, click Make Table.

## Figure 12.17 Select the Output Options

![](img/a858f3b35ed4923af65c22e8829ee5a8_210_1.png)

- Run Order—Lets you designate the order you want the runs to appear in the data table when it is created. Choices are:
- Keep the Same—the rows (runs) in the output table appear as they do in the Design panel.
- Sort Left to Right—the rows (runs) in the output table appear sorted from left to right.
- Randomize—the rows (runs) in the output table appear in a random order.
- Sort Right to Left—the rows (runs) in the output table appear sorted from right to left.
- Randomize within Blocks—the rows (runs) in the output table will appear in random order within the blocks you set up.
- Number of Center Points—Specifies additional runs placed at the center points.
- Number of Replicates—Specify the number of times to replicate the entire design, including centerpoints. Type the number of times you want to replicate the design in the associated text box. One replicate doubles the number of runs.
