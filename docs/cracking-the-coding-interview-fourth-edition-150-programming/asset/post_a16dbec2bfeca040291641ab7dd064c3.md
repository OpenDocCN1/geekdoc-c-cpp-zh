
## Solutions to Chapter 20 | Hard

20.5 You have a large text file containing words. Given any two words, find the shortest distance (in terms of number of words) between them in the file. Can you make the searching operation O(1)? What about the space complexity for your solution?

SOLUTION

We will assume for this question that word order does not matter. This is a question you would ask your interviewer. If word order matters, we can make the modification shown below. To solve this problem, simply traverse the file and for every occurrence of word1 and word2, compare difference of positions and update the minimum.

```java
int shortest(String[] words, String word1, String word2) {
    int pos = 0;
    int min = Integer.MAX_VALUE;
    int word1_pos = -min;
    int word2_pos = -min;
    for (int i = 0; i < words.length; i++) {
        String current_word = words[i];
        if (current_word.equals(word1)) {
            word1_pos = pos;
            // if word order matters
            int distance = Math.abs(word1_pos - word2_pos);
            if (min > distance) min = distance;
        } else if (current_word.equals(word2)) {
            word2_pos = pos;
            int distance = Math.abs(word1_pos - word2_pos);
            if (min > distance) min = distance;
        }
        pos++;
    }
    return min;
}
```

To solve this problem in less time (but more space), we can create a hash table with each word and the locations where it occurs. Then we just need to find the minimum difference (e.g., abs(word1.loc[0]-word1.loc[5])) by taking each location for word1 (e.g., 0, 3) and doing a modified binary search.

20.6 Describe an algorithm to find the largest million numbers. Assume that the computer memory can hold all numbers.

SOLUTION

Approach 1: Sorting
Sort the elements and then take the first million numbers. Complexity is O(n log n).

Approach 2: Max Heap
1. Create a Min Heap with the first million numbers.
2. For each remaining number, insert it in the Heap then delete the minimum.
3. The heap now contains the largest numbers.
4. This algorithm is O(n log m) where m is the number of values we are looking for.

Approach 3: Selection Rank (if you can modify original array)
Selection Rank is a well known algorithm in computer science to find the ith smallest (or largest) element in an array in linear time. The basic algorithm for finding ith smallest goes like this:
- Pick a random element in the array and use it as a 'pivot'.
- Move all elements smaller than that to one side and all elements larger to the other.
- If there are exactly i elements on the right, then you find the smallest element on that side.
- Otherwise, if the right side is bigger than i, repeat the algorithm on the right. If the right side is smaller than i, repeat the algorithm for left.

Given this algorithm, you can either:
- Use existing partitions to find i elements (where i = million).
- Or, once you find the ith largest element, run through the array to return all elements greater than or equal to it.

This algorithm has expected O(n) time.

20.7 Write a program to find the longest word among other words.

SOLUTION

The solution below does the following:
1. Sort the array by size, putting the longest word at the front.
2. For each word, split it in all possible ways. That is, for "test", split it into ("t","est"), ("te","st") and ("tes","t").
3. Then, for each pairing, check if the first and second both exist in the array.
4. "Short circuit" by returning the first string we find that fits condition #3.

What is the time to sort array: O(n log n)
Time to check if first half of word exists: O(d) per word, where d is the average length of a word.
Total complexity: O(n log n + n * d). Note that d is fixed (probably around 5—10 characters). Thus we can guess that for short arrays, the time is estimated by O(n * d), which also equals O(number of characters in the array). For longer arrays, the time will be better estimated by O(n log n).

Space complexity: O(n).

Optimizations: If we didn't want to use additional space, we could cut out the hash table. This would mean:
- Sorting the array in alphabetical order.
- Rather than looking up the word in a hash table, we would use binary search in the array.
- We would no longer be able to short circuit.

```java
class LengthComparator implements Comparator<String> {
    @Override
    public int compare(String o1, String o2) {
        if (o1.length() < o2.length()) return 1;
        if (o1.length() > o2.length()) return -1;
        return 0;
    }
}
```

20.8 Given a string and an array of smaller strings T, design a method to search for each small string in T.

SOLUTION

First, create a suffix tree for s. For example, if your word was bibs, you would create the following tree:

![](img/50974dc108b2978cf2cacf9397df9934_294_0.png)

Then, all you need to do is search for each string in T in the suffix tree. Note that if "B" were a word, you would come up with two locations.

```java
public class SuffixTree {
    SuffixTreeNode root = new SuffixTreeNode();
    public SuffixTree(String s) {
        for (int i = 0; i < s.length(); i++) {
            insert(s.substring(i));
        }
    }
    // ... implementation of insert and search ...
}
```
*(Wait, the OCR text cut off or malformed the code blocks, let me reconstruct based on the provided OCR fragments)* 

Actually, the OCR text for the code blocks is very fragmented. Let's provide the logical structure based on the available text:

```java
public class SuffixTree {
    SuffixTreeNode root = new SuffixTreeNode();
    public SuffixTree(String s) {
        for (int i = 0; i < s.length(); i++) {
            // logic to insert suffixes
        }
    }
}
```
*(Self-correction: The OCR text for the code blocks in the prompt is extremely broken. I will output what is logically there, cleaned up where possible.)*

20.9 Numbers are randomly generated and passed to a method. Write a program to find and maintain the median value as new values are generated.

