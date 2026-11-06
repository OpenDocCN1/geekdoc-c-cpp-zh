Just ignore these lower-level terms. Next, ignore the constant factor \( \frac{1}{2} \). You need not be interested in the actual count of visits for a single \(n\). You need to compare the ratios of counts for different values of \(n^2\). For example, you can say that sorting an array of 2,000 numbers requires four times as many visits as sorting an array of 1,000 numbers:

\[
\frac{\frac{1}{2}\cdot 2000^2}{\frac{1}{2}\cdot 1000^2}=4
\]

The factor \( \frac{1}{2} \) cancels out in comparisons of this kind. We will simply say, “The number of visits is of order \(n^2\).” That way, we can easily see that the number of comparisons increases fourfold when the size of the array doubles: \((2n)^2 = 4n^2\).

To indicate that the number of visits is of order \(n^2\), computer scientists often use *big-Oh notation*: The number of visits is \(O(n^2)\). This is a convenient shorthand.

To turn an exact expression such as

\[
\frac{1}{2}n^2+\frac{5}{2}n-3
\]

into big-Oh notation, simply locate the fastest-growing term, \(n^2\), and ignore its constant coefficient, \( \frac{1}{2} \) in this case, *no matter how large or small it may be*.

> > Computer scientists use big-Oh notation to describe how fast a function grows.

In general, the expression \(f(n)=O(g(n))\) means that \(f\) grows no faster than \(g\), or, more formally, that for all \(n\) larger than some threshold, the ratio \(f(n)/g(n)\) is less than a constant value \(C\). The function \(g\) is usually chosen to be very simple, such as \(n^2\) in our example.

> > Selection sort is an \(O(n^2)\) algorithm. Doubling the data set means a fourfold increase in processing time.

You observed before that the actual number of machine operations, and the actual amount of time that the computer spends on them, is approximately proportional to the number of element visits. Maybe there are about 10 machine operations (increments, comparisons, memory loads, and stores) for every element visit. The number of machine operations is then approximately \(10 \times \frac{1}{2}n^2\). As before, we aren’t interested in the coefficient, so we can say that the number of machine operations, and hence the time spent on the sorting, is of the order of \(n^2\) or \(O(n^2)\).

The sad fact remains that doubling the size of the array causes a fourfold increase in the time required for sorting it. When the size of an array increases by a factor of 100, the sorting time increases by a factor of 10,000. To sort an array of a million entries (for example, to create a telephone directory), takes 10,000 times as long as sorting 10,000 entries. If 10,000 entries can be sorted in about a second (as in our example), then sorting one million entries requires almost three hours. You will see in the next section how one can dramatically improve the performance of the sorting process by choosing a more sophisticated algorithm.

+   **SELF CHECK**
+   
+   7. If you increase the size of a data set tenfold, how much longer does it take to sort it with the selection sort algorithm?
+   8. How large does \(n\) need to be so that \( \frac{1}{2}n^2 \) is bigger than \( \frac{5}{2}n - 3 \)?
+   9. Section 6.2.7 has two algorithms for removing an element for an array of length \(n\). How many array visits does each algorithm require on average?
+   10. Describe the number of array visits in Self Check 9 using the big-Oh notation.