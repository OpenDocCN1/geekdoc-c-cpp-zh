# Theorem 7.12

Any comparison-based algorithm to find the minimum and maximum must use at least \(\lceil 3n/2 \rceil - 2\) comparisons.

# Proof

The basic idea is that if two items are unmarked, the adversary must give out two pieces of information. Otherwise, one of the items has either a W or an L (perhaps both). In that case, with reasonable care, the adversary should be able to avoid giving out two units of information. For instance, if one item, x, has a W and the other item, y, is unmarked, the adversary lets x win again by saying x > y. This gives one unit of information for y but no new information for x. It is easy to see that, in principle, there is no reason that the adversary should have to give more than one unit of information out if there is at least one unmarked item involved in the comparison.

It remains to show that the adversary can maintain values that are consistent with its answers. If both items are unmarked, then obviously they can be safely assigned values consistent with the comparison answer; this case yields two units of information. Otherwise, if one of the items involved in a comparison is unmarked, it can be assigned a value the first time, consistent with the other item in the comparison. This case yields one unit of information.

| x | y | Answer | Information | New x | New y |
|---|---|---|---|---|---|
| - | - | x < y | 2 | L | W |
| | | | 0 | 0 | 1 |
| L | - | x < y | 1 | L unchanged | W x + 1 |
| W or WL | - | x > y | 1 | W or WL unchanged | L x - 1 |
| W or WL | W | x < y | 1 or 0 | WL unchanged | W max(x + 1, y) |
| L or W or WL | L | x > y | 1 or 0 | WL or W or WL unchanged | L min(x - 1, y) |
| WL | WL | consistent | 0 | unchanged | unchanged |
| - | WL | \multicolumn{4}{c}{\multirow{7}{*}{SYMMETRIC TO AN ABOVE CASE}} |
| - | WL | \multicolumn{4}{c}{} |
| - | L | \multicolumn{4}{c}{} |
| L | W | \multicolumn{4}{c}{} |
| L | WL | \multicolumn{4}{c}{} |
| W | WL | \multicolumn{4}{c}{} |

Figure 7.23 Adversary constructs input for finding the maximum and minimum as algorithm runs