# N

The FindLargest algorithm described in the earlier section “Rule 1” has O(N) performance. See that section for an explanation of why it has O(N) performance.

The function N grows more quickly than log(N) and sqrt(N) but still not too quickly, so algorithms that have O(N) performance work quite well in practice.

# N log N

Suppose an algorithm loops over all the items in its problem set and then, for each loop, performs some sort of O(log N) calculation on that item. In that case, the algorithm has O(N × log N) or O(N log N) performance.

Alternatively, an algorithm might perform some sort of O(log N) operation and, for each step it, to do something to the items in the problem.

For example, you have built a sorted tree containing N items as described earlier. You also have an array of N values and you want to know which values in the array are also in the tree.

One approach would be to loop through the values in the array. For each value, you could use the method described earlier to search the tree for that value. The algorithm examines N items and for each it performs log(N) steps the total runtime is O(N log).

Many sorting algorithms that work by comparing items have an O(N log N) runtime. In fact, it can be proven that any algorithm that sorts by comparing items must use at least O(N log N) steps, to this is the best you can do, at least in Big O notation. Some algorithms are faster than others because of the constants Big O notation ignores.

An algorithm that loops over all its inputs and then for each input loops over the inputs having O(N²) performance. For example, the ContainsDuplicates algorithm described earlier, in the section “Rule 4” runs in O(N²) time. See that section for a description and analysis of the algorithm.

Other powers of N, such as O(N³) and O(N⁴), are possible and obviously slower than O(N²).

An algorithm is said to have polynomial runtime if it involves any polynomial involving N. O(N), O(N²), O(N³) and even O(N⁴) are all polynomial runtimes.

Polynomial runtimes are important in some sense these problems can be solved. The exponential and fractal runtimes described next grow extremely quickly, so algorithms that have those runtimes are practical for very small numbers of inputs.