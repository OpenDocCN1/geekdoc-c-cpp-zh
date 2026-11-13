have larger issues to discuss first. The table of the number of operations for each method can now be expressed more concisely, as shown here:

+   - Method 1: 3n
+   - Method 2: n² + 2n
+   - Method 3: ⌊log₁₀n⌋ + 1

# Big-O Notation

The time analyses we gave for the three stair-counting methods were very precise. They computed the exact number of operations for each method. But such precision is sometimes not needed. Often it is enough to know in a rough manner how the number of operations is affected by the input size. In the stair example, we developed the methods thinking about a particular tower, the Eiffel Tower, with a particular number of steps. We expressed our formulas for the operations in terms of n, which stood for the number of steps in the tower. Now suppose that we apply our various stair-counting methods to a tower with 10 times as many steps as the Eiffel Tower. If n is the number of steps in the Eiffel Tower, then this taller tower will have 10n steps. The number of operations needed for Method 1 on the taller tower increases tenfold (from 3n to 3 × (10n) = 30n); the time for Method 2 increases approximately 100-fold (from about n² to about (10n)² = 100n²); and Method 3 increases by only one operation (from the number of digits in n to the number of digits in 10n, or to be very concrete, from the four digits in 2689 to the five digits in 26,890). We can express this kind of information in a format called big-O notation. The symbol O in this notation is the letter O, so big-O is pronounced "big Oh."

We will describe three common examples of the big-O notation. In these examples, we use the notion of "the largest term in a formula." Intuitively, this is the term with the largest exponent on n, or the term that grows the fastest as n itself becomes larger. For now, this intuitive notion of "largest term" is enough. Here are the examples:

Quadratic time. If the largest term in a formula is no more than a constant times n², then the algorithm is said to be "big-O of n²," written O(n²), and the algorithm is called quadratic. In a quadratic algorithm, doubling the input size makes the number of operations increase by approximately fourfold (or less). For a concrete example, consider Method 2, requiring n² + 2n operations. A 100-step tower requires 10,200 operations (that is, 100² + 2 × 100). Doubling the tower to 200 steps increases the time by approximately fourfold, to 40,400 operations (that is, 200² + 2 × 200).

Linear time. If the largest term in a formula is a constant times n, then the algorithm is said to be "big-O of n," written O(n), and the algorithm is called linear. In a linear algorithm, doubling the input size makes the time increase by