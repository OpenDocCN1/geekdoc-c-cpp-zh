
- `SCANDAL?(t)`: We use the *max-scand-time* field to search for this element.
  - If there is no such element in the tree, i.e. *max-scand-time[root] < t*, then return NIL.
  - Otherwise we recursively descend the tree as follows: at each node *n* check whether *max-scand-time[left[n]] > t*. If so recursively descend to the left subtree. Otherwise, check whether *time[n] > t* and *scandalous?[n] = TRUE*. If so return *n*. Otherwise, recursively descend the right subtree.

## Chapter 4

## Dynamic Programming

### 4.1 String Edit Distance

**Problem**

Given two strings and a set of edit operations, design and implement an algorithm to minimize the number of edit operations needed to transform the first string into the second. Please note that matches are not counted.

**Solution**

**Introduction**

Finding the occurrences of a given query string (pattern) from a possibly very large text is an old and fundamental problem in computer science. It emerges in applications ranging from text processing and music retrieval to bioinformatics. This task, collectively known as *string matching*, has several different variations. The most natural and simple of these is *exact string matching*, in which, like the name suggests, one wishes to find only occurrences that are exactly identical to the pattern string. This type of search, however, may not be adequate in all applications if for example the pattern string or the text may contain typographical errors. Perhaps the most important applications of this kind arise in the field of bioinformatics, as small variations are fairly common in DNA or protein sequences.

Other related areas of applications include (but not limited to)

- stochastic transduction
- syntactic pattern recognition
- spelling correction
- string correction
- string similarity
- string classification
- pronunciation modeling
- Switchboard corpus
- string permutations

The field of approximate string matching, which has been a research subject since the 1960's, answers the problem of small variation by permitting some error between the pattern and its occurrences. Given an error threshold and a metric to measure the distance between two strings, the task of approximate string matching is to find all substrings of the text that are within (a distance of) the error threshold from the pattern.

**Edit Distance**

In this solution we concentrate on approximate string matching that uses so called *unit-cost edit distance* as the metric to measure the distance between two strings. *Edit Distance* between the string S_1 and S_2 is defined in general as the minimal cost of any sequence of edit operations that transforms S_1 into S_2 or vice versa.

There are various types of edit distance metrics available:

- *Levenshtein edit distance*: The allowed edit operations are:
  - insertion,
  - deletion, or
  - substitution of a single character,
  
  and each operation has the cost 1. This type of edit distance is sometimes called *unit-cost edit distance*. *Levenshtein edit distance* is perhaps the most common form of edit distance, and often the term edit distance is implicitly assumed to it.

- *Damerau edit distance*: Otherwise identical to the *Levenshtein edit distance*, but allows also the fourth operation of transposing two adjacent characters. A further condition is that the transposed characters must be adjacent before and after the edit operations are applied.

- *Weighted/generalized edit distance*: Allows the same operations as the Levenshtein/Damerau edit distance, respectively, but each operation may have an arbitrary cost.

- *Hamming distance*: Allows only the operation of substituting a character, and each substitution has the unit cost.

- *Longest common subsequence*: Measures the similarity between S1 and S2 by the length of their longest common subsequence. This is in effect equivalent to allowing the edit operations of deleting or inserting a single character with the unit cost.

For the sake of simplicity, we will consider two different kinds of edit distances:

- 1. *Levenshtein edit distance* and
- 2. *Damerau edit distance*.

These two, and especially the *Levenshtein edit distance*, are the most commonly used forms of unit-cost edit distance.

**Levenshtein edit distance**

The unit-cost *Levenshtein edit distance* between the strings S1 and S2 can be defined as the minimum number of single-character insertions, deletions and substitutions needed in transforming S1 into S2 or vice versa.

For example, if S1 = “cat” and S2 = “act”, then there are two ways to transform S1 into S2 with exactly two operations:

- 1. either
  - a) delete S1[1] = ‘c’, i.e., “cat” ⟹ “at”
  - b) insert a ‘c’ between the present S1[1] = ‘a’ and S1[2] = ‘t’, i.e., “at” ⟹ “act”
- 2. or
  - a) substitute S1[1] = ‘c’ with an ‘a’, i.e., “cat” ⟹ “aat”
  - b) and substitute the present S1[2] = ‘a’ with a ‘c’, i.e., “aat” ⟹ “act”

So, in either case, *Levenshtein edit distance*(S1, S2) is 2.

**Damerau edit distance**

In similar fashion, the unit-cost *Damerau edit distance* can be defined as the minimum number of single-character insertions, deletions or substitutions or transpositions between two permanently adjacent characters that are needed in transforming S1 into S2 or vice versa.

Continuing with the same example of strings S1 = “cat” and S2 = “act”, we have that $Damerau\ edit\ distance(S_1,S_2)=1$ as now a single transposition of the characters $S_1[1]='c'$ and $S_1[2]='a'$ is enough to convert $S_1$ into $S_2$, i.e.

$$\text{transpose “ca” in “cat”} \Longrightarrow \text{“act”}$$

Both the Levenshtein and the Damerau edit distance suit well the technique of dynamic programming. We begin by discussing the dynamic programming algorithm for the Levenshtein edit distance.

Let $D(i,j)$ be the edit distance of the strings $S_1[1..i]$ and $S_2[1..j]$, i.e., $D(i,j)$ denotes the minimum number of edit operations needed to transform the first $i$ characters of $S_1$ into the first $j$ characters of $S_2$.

If $S_1$ has $m$ characters and $S_2$ has $n$ characters, then the edit distance is $D(m,n)$.

**Recurrence: Computing the Levenshtein edit distance**

We will compute $D(m,n)$ by solving the more general problem of computing $D(i,j)$ for all combinations of $i$ and $j$, where $i$ ranges from $0$ to $m$ and $j$ ranges from $0$ to $n$.

The base conditions are:

- $D(i,0)=i$, i.e., the only way to transform the first $i$ characters of $S_1$ to $0$ characters of $S_2$ is to delete all the $i$ characters of $S_1$.
- $D(0,j)=j$, i.e., the only way to transform the $0$ characters of $S_1$ to the first $j$ characters of $S_2$ is to insert the $j$ characters of $S_2$ into $S_1$.

Then $D(i,j)$ is the minimum of the following three possibilities:

- 1. $D(i-1,j-1)+\delta(i,j)$, where $\delta(i,j)$ is the cost associated with either substitution cost (or matching zero cost), i.e.,
  - a) $\delta(i,j)=1$ if $S_1[i] \ne S_2[j]$
  - b) $\delta(i,j)=0$ if $S_1[i] = S_2[j]$
- 2. $D(i,j-1)+1$, i.e., deletion cost of the character $S_2[j]$
- 3. $D(i-1,j)+1$, i.e., deletion cost of the character $S_1[i]$

**C++ Implementation**

**Program 4.1: Simple Implementation: Levenshtein edit distance**

```cpp
#include <vector>
#include <algorithm>
#include <cassert>

size_t edit_distance(const std::string & s1,
                     const std::string & s2)
{
    const size_t len1 = s1.size();
    const size_t len2 = s2.size();

    std::vector<std::vector<size_t>>
        d(len1 + 1,
        std::vector<size_t>(len2 + 1));

    d[0][0] = 0;

    for (size_t i = 1; i <= len1; ++i)
    {
        d[i][0] = i;
    }

    for (size_t j = 1; j <= len2; ++j)
    {
        d[0][j] = j;
    }

    for (size_t i = 1; i <= len1; ++i)
    {
        for (size_t j = 1; j <= len2; ++j)
        {
            d[i][j] =
                std::min(
                    std::min(
                        d[i - 1][j] + 1,
                        d[i][j - 1] + 1
                    ),
                    d[i - 1][j - 1] +
                        (s1[i - 1] == s2[j - 1]
                            ? 0 : 1)
                );
        }
    }
    return d[len1][len2];
}

int main()
{
    assert(edit_distance("cat", "act") == 2);
    assert(edit_distance("combo", "coin") == 3);
}
```

**Program 4.2: Improved Implementation: Levenshtein edit distance**

```cpp
#include <vector>
#include <algorithm>
#include <cassert>

size_t levenshtein_distance(
```
