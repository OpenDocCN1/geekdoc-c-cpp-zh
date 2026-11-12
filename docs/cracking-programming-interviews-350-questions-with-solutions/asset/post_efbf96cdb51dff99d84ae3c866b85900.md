
```cpp
}

template <size_t Index, class ElementType, size_t N>
inline const ElementType&
get(const array<ElementType, N>& a)
{
    static_assert(Index < N, "Index out of bounds in std::get<> (const std::array&)");
    return a[Index];
}

template <size_t Index, class ElementType, size_t N>
inline ElementType&&
get(array<ElementType, N>&& a)
{
    static_assert(Index < N, "Index out of bounds in std::get<> (std::array&&)");
    return std::move(a[Index]);
}
```

## 1.10 Seating Problem

### Problem Description

GreedSox, a popular major-league baseball team, is interested in one thing: making money. They have hired you as a consultant to help boost their group ticket sales. They have noticed the following problem. When a group wants to see a ballgame, all members of the group need seats (in the bleacher section), or they go away. Since partial groups can't be seated, the bleachers are often not full. There is still space available, but not enough space for the entire group. In this case, the group cannot be seated, losing money for the GreedSox.

The GreedSox want your recommendation on a new seating policy. Instead of seating people first-come/first-serve, the GreedSox decide to seat large groups first, followed by smaller groups, and finally singles (i.e., groups of 1).

You are given a set of groups, $G[1..m] = [g_1, g_2, \ldots, g_m]$, where $g_i$ is a number representing the size of the group. Assume that the bleachers seat n people. Consider the following greedy seating algorithm, where the function ADMIT(i) admits group i, and REJECT(i) sends away group i.

### Algorithm 15 Seat Algorithm

```text
1: function SEAT(G[1..m], n)
2:     admitted ← 0
3:     G ← SORT(G)                    ▷ Sort groups largest to smallest.
4:     for i ← 1 to m do
5:         if G[i] ≤ n then
6:             ADMIT(i)
7:             n ← n - G[i]
8:             admitted ← admitted + G[i]
9:         else
10:            REJECT(i)
11:        end if
12:    end for
13:    return admitted
14: end function
```

The seat algorithm first sorts the groups by size. It then iterates through the groups from largest to smallest, seating any group that fits in the bleachers. It returns the number of people admitted.

- 1. The GreedSox owners are right: the greedy seating algorithm works pretty well. Show that if, given G and n, it is possible to admit k people, then the greedy seating algorithm admits at least k/2 people.
- 2. Unfortunately, the seat algorithm does not work perfectly. Show that seat is not optimal by giving a counterexample in which, asymptotically as n gets large, the ratio between greedy seating and optimal seating approaches 1/2.

When you present your results to the GreedSox owners, they point out the following problem: unlike numbers in a computer's memory, real people are hard to move around. In particular, people waiting in line do not like to be sorted. The GreedSox owners ask you to develop a version of the greedy seating algorithm that does not modify the set G. (You can think of G as being stored in read-only memory.) You suggest the following algorithm:

### Algorithm 16 ReSeat Algorithm

```text
1: function RESEAT(G[1..m], n)
2:     admitted ← 0
3:     for j ← 1 to ⌈log n⌉ do
4:         for i ← 1 to m do
5:             if G[i] ≥ n/2^j and G[i] ≤ n then
6:                 ADMIT(i)
7:                 n ← n - G[i]
8:                 admitted ← admitted + G[i]
9:             else if G[i] > n then
10:                REJECT(i)
11:            end if
12:        end for
13:    end for
14:    return admitted
15: end function
```

The RESEAT algorithm iterates through the list of groups several times. In the first iteration, it admits any group of size at least n/2. In the second iteration, it admits any group of size at least n/4. It continues in the same manner seating smaller and smaller groups until the theater is filled. When RESEAT finishes, it returns the number of people admitted.

- 3. Assume that, given G and n, it is possible to admit at least k people. Show that the RESEAT algorithm still seats at least k/2 people.
- 4. The RESEAT algorithm runs in O(m log n) time. Devise a new algorithm that runs in O(m) time and still guarantees that if k people can be seated, your algorithm seats at least k/2 people.

### Solution

- 1. We begin by proving a lemma about the number of people admitted by the SEAT algorithm.

**Lemma 1**

Algorithm SEAT either admits all groups of *size* ≤ n, or it *admits* ≥ n/2 people.

**Proof** Assume algorithm SEAT does not admit all groups of *size* ≤ n. That is, there is some group $g_i$ of *size* ≤ n that SEAT does not admit.

There are two cases to consider. First, assume that $g_i \geq n/2$. Then, since the algorithm is greedy, we know that it must have admitted some group larger than $g_i$; otherwise, group $g_i$ would have been admitted. Therefore, we can conclude that the algorithm seats $\geq \frac{n}{2}$ people, as required.

For the second case, assume that $g_i < \frac{n}{2}$. Since $g_i$ is not admitted, we know that at some point $\mathrm{remaining} < \frac{n}{2}$. Since remaining is non-increasing, we thus conclude that at least $\frac{n}{2}$ people are seated.

We argue that this lemma immediately implies that the SEAT algorithm is 2-competitive. First, if SEAT admits all groups of size ≤ n, then it admits exactly the same number of people as the optimal seating algorithm. Second, if SEAT admits at least $\frac{n}{2}$ people, we know that the optimal seating algorithm can seat at most $n$ people. Hence $\frac{n}{2} \geq \frac{k}{2}$, as required.

- 2. Consider groups $G = \left\{\frac{n+2}{2}, \frac{n}{2}, \frac{n}{2}\right\}$. Notice that the greedy seating algorithm admits the group of $\frac{n+2}{2}$, and then cannot admit any of the other groups. The optimal algorithm admits the two groups of size $\frac{n}{2}$, filling all $n$ seats. Notice that asymptotically $\frac{(n+2)/2}{n}$ approaches $\frac{1}{2}$ as $n$ gets large.

- 3. The argument in this case is quite similar to the proof in the first part. We begin by reproving the same lemma above about the number of people admitted by the algorithm RESEAT.

**Lemma 2**

Algorithm RESEAT either admits all groups of size ≤ n, or it admits ≥ $\frac{n}{2}$ people.

**Proof** Assume algorithm RESEAT does not admit all groups of size ≤ n. That is, there is some group $g_i$ of size ≤ n that RESEAT does not admit.

There are two cases to consider. First, assume that $g_i \geq \frac{n}{2}$. Then, since the algorithm first considers all groups of size $\geq \frac{n}{2}$ (when $j=1$), we know that it must have admitted some group of size $\geq \frac{n}{2}$; otherwise, group $g_i$ would have been admitted in the loop when $j=1$. Therefore, we can conclude that the algorithm seats $\geq \frac{n}{2}$ people, as required.

For the second case, assume that $g_i < \frac{n}{2}$. Notice that when $j=\lceil\log n\rceil$, $g_i \geq \frac{n}{2^j}$. Therefore, if $g_i$ is not admitted, we can conclude that at some point $\mathrm{remaining} < g_i$. That is, $\mathrm{remaining} < g_i < \frac{n}{2}$. Since remaining is non-increasing, we thus conclude that at least $\frac{n}{2}$ people are seated.

As before, this lemma immediately implies that the algorithm RESEAT is 2-competitive, as desired.

### Algorithm 17 ReSeat Linear Time Algorithm

```text
1: function FAST-RESEAT(G[1...m], n)
2:     admitted ← 0
3:     remaining ← n
4:     for i ← 1 to m do
5:         if G[i] ≥ n/2 and G[i] ≤ remaining then
6:             ADMIT(i)
7:             admitted ← admitted + G[i]
8:             remaining ← remaining − G[i]
9:         end if
10:    end for
11:    for i ← 1 to m do
12:        if G[i] ≤ remaining then
13:            ADMIT(i)
14:            admitted ← admitted + G[i]
15:            remaining ← remaining − G[i]
16:        end if
17:    end for
18:    return admitted
19: end function
```

The argument showing this algorithm is correct is essentially the same as the proof in the third part. In particular, we again show the same lemma about the number of people seated.

**Lemma 3**

Algorithm FAST-RESEAT either admits all groups of size ≤ n, or it admits ≥ n/2 people.

**Proof** Assume algorithm FAST-RESEAT does not admit all groups of size ≤ n. That is, there is some group $g_i$ of size ≤ n that FAST-RESEAT does not admit.

There are two cases to consider. First, assume that $g_i \geq n/2$. Then, since the algorithm first considers all groups of size ≥ n/2, we know that if $g_i$ was rejected, it must have admitted some group of size ≥ n/2; otherwise, group $g_i$ would have been admitted. Therefore, we can conclude that the algorithm seats ≥ n/2 people, as required.

For the second case, assume that $g_i < n/2$. If $g_i$ is not admitted, we can conclude that $g_i > \mathrm{remaining}$. That is, $\mathrm{remaining} < g_i < n/2$.
