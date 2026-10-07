# 210 7.5 Zero-sum games

from $[r, p, s]$. They then look up the matrix entry corresponding to their moves, and Column pays Row's gain and Column's loss.

$G = \begin{array}{c|ccc} & r & p & s \ \hline Row & 0 & -1 & 1 \ p & 1 & 0 & -1 \ s & -1 & 1 & 0 \end{array}$

Now suppose the two of them play this game repeatedly. If Row always makes the same move, Column will quickly catch on and will always play the counter, winning every time. Row might mix things up; we can model this by allowing Row to have a *mixed strategy*, in which on each turn she plays $r$ with probability $x_1, p$ with probability $x_2$, and $s$ with probability $x_3$. This strategy is specified by the vector $\mathbf{x} = (x_1, x_2, x_3)$, positive numbers that add up to 1. Similarly, Column's mixed strategy is $y=(y_1, y_2, y_3)$.

On any given round of the game, there is $x_iy_j$ chance that Row and Column will play the $i$-th and $j$-th moves, respectively. Therefore the expected (average) payoff is

$$\sum_{i,j} G_{ij} \cdot \text{Row[Row plays $i$, Column plays $j$]} = \sum_{i,j} G_{ij}x_iy_j$.

Row wants to *maximize*, while Column wants to *minimize*. What payoffs do they hope to achieve in rock-paper-scissors? Well, suppose for instance Row plays the "completely random" strategy $\mathbf{x} = (1/3, 1/3, 1/3)$. If Column plays $r$, then the average payoff (reading the first column of the matrix mix) will be

$$\frac{1}{3} \cdot 0 + \frac{1}{3} \cdot 1 + \frac{1}{3} \cdot -1 = 0$.

This is also true if Column plays $p$, and the payoff of any mixed strategy $(y_1, y_2, y_3)$ is just a weighted average of the individual payoffs for playing $r, p$, and $s$, it must also be so. This can be seen directly from the preceding formula,

$$\sum_{i,j} G_{ij}x_iy_j = \sum_{i,j} G_{ij}y_j = \sum_{j} y_j(\sum_{i} G_{ij}) = \sum_{j} y_j \cdot 0 = 0$.

where the second-to-last equality is the observation that every column of $G$ adds up to zero. By playing the "completely random" strategy, Row forces an expected payoff of zero, no matter what Column does. This means Column cannot hope for a negative (expected) payoff (remember that she wants the payoff to be as small as possible). But symmetrically, if Column plays the completely random strategy, she also forces an expected payoff of zero, and Row cannot hope for a positive (expected) payoff. In short, the each player can do is to play completely

> $^2$Also of interest are scenarios in which players alter their strategies from round to round, but these can get very complicated and are a vast subject unto themselves.