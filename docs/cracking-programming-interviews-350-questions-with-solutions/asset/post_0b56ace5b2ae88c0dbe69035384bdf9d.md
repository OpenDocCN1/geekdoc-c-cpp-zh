
## Complexity

At most 3(n - 1) questions will be asked:

- 1. n - 1 questions in the first phase to eliminate n - 1 persons, and then
- 2. at most 2(n - 1) questions to verify that the candidate is indeed a celebrity.

Notice that the size of the input is not n, but rather n(n - 1), which is the number of entries of the matrix. This solution shows that it is possible to identify a celebrity by looking at only O(n) entries in the adjacency matrix, even though a priori the solution may be sensitive to each of the n(n - 1) entries.

## Remarks

The key idea in this elegant solution is to reduce the size of the problem from n to n - 1 in a clever way. Do not start by simply considering an arbitrary input of size n - 1 and attempting to extend it. Select a particular input of size n - 1.

## Uniqueness of Celebrity

> In a set S of n people, there can be only one celebrity.

Assume for contradiction that there are two celebrities C₁ and C₂ in S. By definition of celebrity, everyone knows a celebrity. Therefore ∀a ∈ S − {C₁}, a knows C₁. Because C₂ ∈ S − {C₁}, C₂ knows C₁. But celebrities don't know anyone. Therefore, C₂ is not a celebrity. This contradicts our assumption that C₂ was a celebrity. Therefore the assumption is false. Therefore, we cannot have two celebrities.

The first algorithm is based on a brute-force approach. We essentially look at each pair of people to see if they know each other. If we find a person that knows nobody but is known by all the others, that person is a celebrity:

```text
Algorithm 34 Celebrity Algorithm Brute Force
1: Input : set S of n people
2: Output : a celebrity, or _no celebrity_ if there is no celebrity.
3: for all A ∈ S do
4:     for all B ∈ S − {A} do
5:         if A knows B then
6:             Break out of inner loop
7:         else
8:             C ← A
9:         end if
10:    end for
11: end for
12: for all α ∈ S do
13:    if α does not know C then
14:        return “No Celebrity”
15:    end if
16:    return C
17: end for
```

This algorithm runs in O(n^2) time. Can we do better? Yes, we can. The following algorithm is based on the observation that by asking a single question, we can eliminate a person as a possible celebrity. So, if I ask “Does A know B?” and the answer is “no”, then B cannot be a celebrity, because a celebrity must be known by everybody else. On the other hand, if the answer is “yes”, then A cannot be a celebrity because a celebrity knows nobody. Therefore, with a single question “Does A know B?”, we learn something no matter what the answer to the question is. This leads to this algorithm:

```text
Algorithm 35 Celebrity Algorithm Optimized
1: Input : set S of n people
2: Output : a celebrity, or no celebrity if there is no celebrity.
3: Candidates ← S
4: while |Candidates| > 1 do
5:     Choose A and B | A ∈ Candidates and B ∈ Candidates
6:     if A knows B then
7:         Candidates ← Candidates - {A}
8:     else
9:         Candidates ← Candidates - {B}
10:    end if
11: end while
12: Let C be the only remaining element of Candidates
13: for all α ∈ S - {C} do
14:     if α does not know C or C knows α then
15:         return "No Celebrity"
16:     end if
17:     return C
18: end for
```

The first loop here runs *n - 1* times because every time around the loop we eliminate a possibility (and we stop when there is one possibility left). The second loop runs for *n - 1* times also because we let α take on |S| - 1 different values. Therefore the overall running time is in O(n).

The elimination phase maintains a list of possible celebrities. Initially it contains all n people. In each iteration, we delete one person from the list. We exploit the following key observation: *if person 1 knows person 2, then person 1 is not a celebrity; if person 1 does not know person 2, then person 2 is not a celebrity.* Thus, by asking person 1 if he knows person 2, we can eliminate either person 1 or person 2 from the list of possible celebrities. We can use this idea repeatedly to eliminate all people but one, say person p. We now verify by brute force whether p is a celebrity: for every other person i, we ask person p whether he knows person i, and we ask person i whether they know person p. If person p always answers no, and the other people always answer yes, then we declare person p as the celebrity. Otherwise, we conclude there is no celebrity in this group.

## Correctness

During the elimination phase, we maintain the invariant that if there exists a celebrity, the celebrity is on the list. We can prove this by induction on the number of iterations. Thus, when elimination phase ends, either person p is a celebrity or there is no celebrity. The elimination phase requires exactly n - 1 questions, since each question reduces the size of the list by 1. In the verification phase, we ask n − 1 questions, and we ask the other n − 1 people one question. This phase requires at most 2(n − 1) questions, possibly fewer if person p is not a celebrity. So the total number of questions is 3(n − 1). To efficiently implement the elimination phase, we maintain a queue that contains the remaining candidates. Initially, we insert all n people to the queue. At each iteration we remove the top two elements off the queue, say v and w, and ask v whether he (or she) knows w. Depending on the outcome, we either insert v or w at the end of the queue. Each queue operation takes Θ(1) time, so the whole process takes Θ(n) time.

## An even better solution

We note that it is possible to save an additional log² n questions in the verification phase by not repeating any questions we already asked during the elimination phase. By maintaining the elements in a queue, the celebrity is involved (i.e., either asked or asked about) at least log² n questions during the elimination phase. This explains why we chose a queue instead of a stack. Also, it is not hard to see that any algorithm must ask at least 2(n − 1) questions if there exists a celebrity, since we must verify that the celebrity does not know anyone, and that everyone knows the celebrity.

## C++11 Implementation

*Program 1.29: Finding Celebrity Program*

```cpp
#include <iostream>
#include <stack>
#include <array>

template <int n, int m>
using CelebrityMatrix =
    std::array<std::array<bool, n>, m>;

// Person with 2 is the celebrity
CelebrityMatrix<4, 4> KnowCeleb =
{
    0, 0, 1, 0,
    0, 0, 1, 0,
    0, 0, 1, 0,
    0, 0, 1, 0
};

template<int Size>
int FindCelebrity()
{
    // Handle trivial case of size = 2
    std::stack<int> person_stack;

    int i;
    int C; // Celebrity
    i = 0;
    while(i < Size)
    {
        person_stack.push(i);
        i = i + 1;
    }

    int A = person_stack.top();
    person_stack.pop();

    int B = person_stack.top();
    person_stack.pop();

    while(person_stack.size() != 1)
    {
        if( KnowCeleb[A][B] )
        {
            A = person_stack.top();
            person_stack.pop();
        }
        else
        {
            B = person_stack.top();
            person_stack.pop();
        }
    }

    // Potential celebrity candidate
    C = person_stack.top();
    person_stack.pop();

    // Last candidate was not examined,
    // it leads one excess comparison (optimize)
    if (KnowCeleb[C][B])
        C = B;

    if (KnowCeleb[C][A])
        C = A;

    i = 0;
    while(i < Size)
    {
        if(C != i)
            person_stack.push(i);
        i = i + 1;
    }

    while(!person_stack.empty())
    {
        i = person_stack.top();
        person_stack.pop();

        // C must not know i
        if (KnowCeleb[C][i])
            return -1;

        // i must know C
        if (!KnowCeleb[i][C])
            return -1;
    }

    return C;
}

int main()
{
    int id = FindCelebrity<4>();

    id == -1 ? std::cout << "No celebrity" : std::cout << "Celebrity ID " << id;
}
```

## 1.19 Transport Problem

### Problem Description

Let $C_1,C_2,\ldots,C_n$ be $n$ cities placed along a straight line. Let $d_i$ be the distance between $C_i$ and $C_{i+1}$, for $1 \leq i < n$. Initially each city $C_i$ possesses some amount $x_i \in \mathbb{R}$ of a certain resource, say water. If $x_i < 0$, what $C_i$ possesses is not real water but deficiency of water, e.g. if $C_i$ has -5.5 units of water and afterwards we transport 6 units of water to it, it is going to have +0.5 units. Each $C_i$ needs some amount $l_i \in \mathbb{R}^+$ of water. We say $C_i$ is satisfied $\Longleftrightarrow l_i \leq x_i$.

Water can be transported between any two adjacent cities but the transportation is lossy: if we start transporting amount $z$ from $C_i$ to $C_{i+1}$ or vice versa, the amount that is going to be delivered is $\max\{z-d_i,0\}$.

Design an algorithm that outputs TRUE, in case there is a way to transport water between the cities so that every city is satisfied, or FALSE, otherwise. Assume that the amount of water in any city is constant unless water is transported to, or from, it. Prove the correctness of your algorithm and analyze its time complexity.

### Solution

Define $d_\pi$ to be zero. Consider the following algorithm:
