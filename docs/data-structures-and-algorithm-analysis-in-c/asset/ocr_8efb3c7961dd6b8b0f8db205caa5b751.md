elements in the group. We will let $H$ represent the *huge* elements. These are elements that are known to be larger than a large median. Similarly, $T$ represents the *tiny* elements, which are smaller than a small median. There are 10 elements of type $H$: Two are in each of the groups with an $L$ type median, and two elements are in the same group as $v$. Similarly, there are 10 elements of type $T$.

Elements of type $L$ or $H$ are guaranteed to be larger than $v$, and elements of type $S$ or $T$ are guaranteed to be smaller than $v$. There are thus guaranteed to be 14 large and 14 small elements in our problem. Therefore, a recursive call could be on at most $45 - 14 - 1 = 30$ elements.

Let us extend this analysis to general $N$ of the form $10k + 5$. In this case, there are $k$ elements of type $L$ and $k$ elements of type $S$. There are $2k + 2$ elements of type $H$, and also $2k + 2$ elements of type $T$. Thus, there are $3k + 2$ elements that are guaranteed to be larger than $v$ and $3k + 2$ elements that are guaranteed to be smaller. Thus, in this case, the recursive call can contain at most $7k + 2 < 0.7N$ elements. If $N$ is not of the form $10k + 5$, similar arguments can be made without affecting the basic result.

It remains to bound the running time to obtain the pivot result. There are two basic steps. We can find the median of five elements in constant time. For instance, it is not hard to sort five elements in eight comparisons. We must do this $\lceil N/5 ceil$ times, so this step takes $O(N)$ time. We must then compute the median of a group of $\lceil N/5 ceil$ elements. The obvious way to do this is to sort the group and return the element in the middle. But this takes $O(\lceil N/5 ceil \log(\lceil N/5 ceil)) = O(N \log N)$ time, so this does not work. The solution is to call the selection algorithm recursively on the $\lceil N/5 ceil$ elements.

This completes the description of the basic algorithm. There are still some details that need to be filled in if an actual implementation is desired. For instance, duplicates must be handled correctly, and the algorithm needs a cutoff large enough to ensure that the recursive calls make progress. There is quite a large amount of overhead involved, and this algorithm is not practical at all, so we will not describe any more of the details that need to be considered. Even so, from a theoretical standpoint, the algorithm is a major breakthrough, because, as the following theorem shows, the running time is linear in the worst case.

# Theorem 10.9

The running time of quickselect using median-of-median-of-five partitioning is $O(N)$.

# Proof

The algorithm consists of two recursive calls of size $0.7N$ and $0.2N$, plus linear extra work. By Theorem 10.8, the running time is linear.

# Reducing the Average Number of Comparisons

Divide and conquer can also be used to reduce the expected number of comparisons required by the selection algorithm. Let us look at a concrete example. Suppose we have a group, $S$, of 1,000 numbers and are looking for the 100th smallest number, which we will call $X$. We choose a subset, $S'$, of $S$ consisting of 100 numbers. We would expect that the value of $X$ is similar in size to the 10th smallest number in $S'$. More specifically, the fifth smallest number in $S'$ is almost certainly less than $X$, and the 15th smallest number in $S'$ is almost certainly greater than $X$.