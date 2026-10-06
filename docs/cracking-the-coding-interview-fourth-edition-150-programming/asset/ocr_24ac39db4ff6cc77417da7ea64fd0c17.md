# Solutions to Chapter 20 | Hard

20.7 Write a program to find the longest word of other words. pg 91

# SOLUTION

The solution below does the following:

+   1. Sort the array by size, putting the longest word at the front

+   2. For each word, split it in all possible ways. That is, for "test", split it into ("t","est"), ("te","st") and ("tes","t"). only word order works perfectly for unordered pairs!

+   3. Then, for each pairing, check if the first half and the second both exist in the array. not what we want; this is what is requested!

+   4. "Short circuit" by returning the first string we find that fits condition #3.

What is the time to sort array: O(n log n)

Time to check if first / second half of word exists: O(d) per word, where d is the average length of a word.

Total complexity: O(n log n + n * d). Note that d is fixed (probably around 5—10 characters). Thus, we can guest that for short arrays, the time is estimated by O(n * d), which also equals O(number of characters in the array). For longer arrays, the time will be better estimated by O(n log n).

Space complexity: O(n).

Optimizations: If we didn't want to use additional space, we could cut out the hash table. This would mean: did not use hash table above

+   Sorting the array in alphabetical order

+   Rather than looking up the word in a hash table, we would use binary search in the array

+   We would no longer be able to short circuit.

```
class LengthComparator implements Comparator<String> {
    @Override
    public int compare(String o1, String o2) {
        if (o1.length() < o2.length()) return 1;
        if (o1.length() > o2.length()) return -1;
        return 0;
    }
}
```