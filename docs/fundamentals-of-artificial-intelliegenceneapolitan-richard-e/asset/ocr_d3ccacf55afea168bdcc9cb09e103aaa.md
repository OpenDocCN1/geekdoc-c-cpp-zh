![](bbox=[0.25, 0.08, 0.76, 0.4])

# Figure 15.4 A table for constructing the solution to parsing the sentence “y x x x x.”

y x x x x.

We develop an n x n table where n is the number of words in the sentence (n = 5 in this example), and we construct our solution in the lower-right part of the table. Such a table T appears in Figure 15.4. We construct the solution by filling in diagonals 1, 2, 3, 4, and 5 in sequence. The sentence appears on the edges of diagonal 1. The values for diagonal 1 are computed directly from the words in the sentence. For each of the other diagonals, the value for T[i, j] is determined from the elements in row i that are left of T[i, j] and the values in column j that are above T[i, j]. For example, suppose that we are determining the value of T[2, 5]. Figure 15.4 shows how that value is determined from values in row 2 and column 5. The far-left item in row 2 (the one in column 2) is combined with the closest item in column 5 (the one in row 3). Then the next item in row 2 (the one in column 3) is combined with the next item in column 5 (the one in row 4). Finally, the closest item in row 2 (the one in column 4) is combined with the farthest item in column 5 (the one in row 5). The results of all these combinations determines the value of T[2, 5].

Next we walk through the algorithm using the sentence “y x x x x,” show how the values are combined, and along the way explain why this results in the solution finally appearing in T[1, 5].

To determine the values in diagonal 1 we visit each array slot in that diagonal in sequence. When visiting the first one (T[1, 1]), we find a “y” on it edge (see Figure 15.5 (a)). We then look at the rules in grammar and see which nonterminals can yield a “y”. The only such nonterminal is A; so we place an