
- It shall always walk in the direction in which it is looking.
- It shall only alter its direction of looking at the points \(P_i\), namely by performing a clockwise rotation of \(\alpha\): \(0 \leq \alpha < 2\pi\).
- It shall end in \(P_0\), while looking towards \(P_1\).

As a consequence of this walk the robot has made a clockwise rotation which is a multiple of \(2\pi\).

Write a program to compute this multiple, under the additional requirement that all expressions and variables occurring in the program have to be of integer or of boolean type.

## Solution

A first inspection of the problem tells us that the requested answer does not change whenever the set of points is translated through the plane. Only the relative position of each pair of successive points plays a role in the determination of the answer.

Therefore we introduce the vectors \(\vec{u}_i\), to be defined as \(\vec{u}_i=(P_i \to P_{i+1})\) for \(0 \leq i \leq 47\), where \(P_{47}=P_0\) and \(P_{48}=P_1\).

The direction of looking during the walk from \(P_i\) to \(P_{i+1}\) then equals \(\vec{u}_i\). Hence the successive directions of looking during the robot's walk are \(\vec{u}_0,\vec{u}_1,\vec{u}_2,\ldots,\vec{u}_{46},\vec{u}_{47}(=\vec{u}_0)\).

The clockwise rotation in the point \(P_i\) towards \(P_{i+1}\) now corresponds to a clockwise rotation from \(\vec{u}_{i-1}\) to \(\vec{u}_i\).

Since in the initial state the robot looks in the same direction as in the final state, it is suggested to take this direction as reference direction. And then the final answer will be equal to the total number of times that, during its rotation, the robot's eye passes this reference direction.

A more precise and more manageable formulation of the problem is at hand as soon as we realize that the answer does not change either if the set of points is rotated inside the plane. This has as a consequence that any direction \(\vec{r}\) can be taken as a reference direction.

If we define \(\theta(\vec{u}_i): 0 \leq \theta(\vec{u}_i) < 2\pi\) to be the angle of the clockwise rotation from \(\vec{r}\) to \(\vec{u}_i\), then the final answer \(p\) will have to satisfy

$$p = \#\{i \mid 0 \leq i < 47,\ \theta(\vec{u}_{i+1}) < \theta(\vec{u}_i)\}.$$

Based on the above, our program is:

```
1: j ← 0
2: p ← 0
3: while j ≠ 47 do
4:     if θ(u_{j+1}) < θ(u_j) then
5:         p ← p + 1
6:     else if θ(u_{j+1}) ≥ θ(u_j) then
7:         skip
8:     end if
9:     j ← j + 1
10: end while
```

If the computation of \(\theta\) is felt to be expensive, we can introduce \(\alpha = \theta(\vec{u}_0)\), then the program is

```
1: j ← 0
2: p ← 0
3: α ← θ(u_0)
4: while j ≠ 47 do
5:     j ← j + 1
6:     β ← θ(u_j)
7:     if β < α then
8:         p ← p + 1
9:     else if β ≥ α then
10:        skip
11:    end if
12:    α ← β
13: end while
```

A next remark is that, in fact, we do not want to compute the angles \(\alpha\) and \(\beta\), but just to compare them.

Comparing two angles \(\alpha\) and \(\beta\) is fairly easy in the case that \(0 \leq \alpha < \pi/2\) and \(0 \leq \beta < \pi/2\), because then \(\beta < \alpha\) is equivalent to \(\tan(\beta) < \tan(\alpha)\), tangents being compared at the expense of two simple multiplications, when points are given in a Cartesian coordinate system.

Comparing two angles \(\alpha\) and \(\beta\) is not so difficult either in general case, if we are willing to represent \(\alpha\) and \(\beta\) in the angle system with base \(\pi/2\):

$$\alpha = a \times \frac{\pi}{2} + \alpha', \qquad 0 \leq \alpha' < \frac{\pi}{2}$$
$$\beta = b \times \frac{\pi}{2} + \beta', \qquad 0 \leq \beta' < \frac{\pi}{2}$$

Then, the inequality \(\beta < \alpha\) is equivalent to

$$b < a \text{ or } (b = a \text{ and } \beta' < \alpha')$$

which in turn is equivalent to

$$b < a \text{ or } (b = a \text{ and } \tan(\beta') < \tan(\alpha'))$$

Now, the program is:

```
1: j ← 0
2: p ← 0
3: a : a × π/2 + α' = θ(u_0)
4: α' : 0 ≤ α' < π/2
5: while j ≠ 47 do
6:     j ← j + 1
7:     b : b × π/2 + β' = θ(u_j)
8:     β' : 0 ≤ β' < π/2
9:     if b < a or (b = a and tan(β') < tan(α')) then
10:        p ← p + 1
11:    else if b > a or (b = a and tan(β') ≥ tan(α')) then
12:        skip
13:    end if
14:    a ← b
15:    α' ← β'
16: end while
```

Looking for a simple initialization of \(a\) and \(\alpha'\), it seems attractive to choose \(\vec{r} = \vec{u}_0\) as a reference direction, but in that case the computations of \(\beta'\) and of \(\tan(\beta') < \tan(\alpha')\) become rather cumbersome. With respect to these later computations, there is hardly another possibility than taking one of the four coordinate directions as reference direction \(\vec{r}\). The choice being immaterial on account of symmetry, we shall select the negative \(y\)-axis.

Now we switch back in our representation from angles to vectors, because in order to compute \(\tan(\alpha')\) and \(\tan(\beta')\), it is convenient to have two vectors \((u_x,u_y)\) and \((v_x,v_y)\) respectively, such that

$$\theta(u_x,u_y)=\alpha'$$

and

$$\theta(v_x,v_y)=\beta'$$

Then \(\tan(\beta') < \tan(\alpha')\) is coded as

$$-\frac{v_x}{v_y} < -\frac{u_x}{u_y}$$

or, preferably, as \(v_x u_y < u_x v_y\).

In order to achieve that \(0 \leq \beta' < \frac{\pi}{2}\), we have to achieve that \(v_x \leq 0\) and \(v_y < 0\). In order to compute \(b\) we have to investigate counterclockwise turns of \(\frac{\pi}{2}\) of the vector \(\vec{u}_i\).

Now we obtain, for \(b\) and \(\beta'\) with \(b \times \frac{\pi}{2} + \beta' = \theta(\vec{u}_i)\) and \(0 \leq \beta' < \frac{\pi}{2}\), the following piece of code:

```
1:  vx ← x[j + 1] − x[j]
2:  vy ← y[j + 1] − y[j]
3:  b ← 0
4:  while vx > 0 or vy ≥ 0 do
5:      vx ← −vy
6:      vy ← vx
7:      b ← b + 1
8:  end while
```

The initialization of \(a\) and \(\alpha'\) can become quite simple if we succeed in finding some vector \(\vec{u}_{-1}\) such that \(\theta(\vec{u}_i) > \theta(\vec{u}_{-1})\), because then our final result can be written as

$$p = \#\{i \mid -1 \leq i < 47,\ \theta(\vec{u}_{i+1}) < \theta(\vec{u}_i)\}$$

and the loop invariant as

$$p = \#\{i \mid -1 \leq i < j,\ \theta(\vec{u}_{i+1}) < \theta(\vec{u}_i)\}, \qquad -1 \leq j \leq 47.$$

We hardly have any choice, because \(\vec{u}_{-1}\) must be defined such that \(\theta(\vec{u}_{-1}) = 0\) (it could coincide with the negative \(y\)-axis), for instance \(\vec{u}_{-1} = (0,-1)\). Then the initialization of \(a\) and \(\alpha'\) results in:

```
ux ← 0
uy ← −1
a ← 0
```

To implement the extra points \(P_{47}\) and \(P_{48}\), we introduce an auxiliary variable \(h \leftarrow (j+1) \bmod 47\), by means of which we can round the arrays.

## Algorithm 46 Robot Walk Algorithm

```
1: j ← −1
2: h ← 0
3: p ← 0
4: ux ← 0
5: uy ← −1
6: a ← 0
7: while j ≠ 47 do
8:   j ← j + 1
9:   h0 ← h
10:  h ← (j + 1) mod 47
11:  vx ← x[h] − x[h0]
12:  vy ← y[h] − y[h0]
13:  b ← 0
14:  while vx > 0 or vy ≥ 0 do
15:    vx ← −vy
16:    vy ← vx
17:    b ← b + 1
18:  end while
19:  if b < a or (b == a and vx × uy < ux × vy) then
20:    p ← p + 1
21:  else if b > a or (b == a and vx × uy ≥ ux × vy) then
22:    skip
23:  end if
24:  ux ← vx
25:  uy ← vy
26:  a ← b
27: end while
```

## 2.8 Linear Time Sorting

### Problem

Given an array of integers, where different integers may have different numbers of digits, but the total number of digits over all the integers in the array is \(n\). Show how to sort the array in \(O(n)\) time.

### Solution

The usual, unadorned radix sort algorithm will not solve this problem in the required time bound. The number of passes, \(d\), would have to be the number of digits in the largest integer.

Suppose that there are \(m\) integers; we always have \(m \leq n\). In the worst case, we would have one integer with \(n/2\) digits and \(n/2\) integers with one digit each. We assume that the range of a single digit is constant.

Therefore, we would have \(d = \frac{n}{2}\) and \(m = \frac{n}{2} + 1\), and so the running time would be \(d m = \Theta(n^2)\).

Let us assume without loss of generality that all the integers are positive and have no leading zeros. If there are negative integers or 0, deal with the positive numbers, negative numbers, and 0 separately.

Under this assumption, we can observe that integers with more digits are always greater than integers with fewer digits. Thus, we can first sort the integers by number of digits using counting sort, and then use radix sort to sort each group of integers with the same length. Noting that each integer has between 1 and \(n\) digits, let \(m_i\) be the number of integers with \(i\) digits, for \(i = 1, 2, \ldots, n\). Since there are \(n\) digits altogether, we have

$$\sum_{i=1}^{n} i \times m_i = n.$$

It takes \(O(n)\) time to compute how many digits all the integers have and, once the numbers of digits have been computed, it takes \(O(m + n) = O(n)\) time to group the integers by their number of digits. To sort the group of integers with exactly \(i\) digits by radix sort takes \(\Theta(i \times m_i)\) time. The time to sort all groups, therefore, is

$$\sum_{i=1}^{n} \Theta(i \times m_i) = \Theta\left(\sum_{i=1}^{n} i \times m_i\right) = \Theta(n).$$

## 2.9 Write as Sum of Consecutive Positive Numbers

### Problem Description

Given a positive integer \(N\), write a program to determine the number of ways in which \(N\) can be written as the sum of consecutive positive integers.

### Solution

We observe that for each positive \(k\), the number of ways in which \(N\) can be written as the sum of exactly \(k\) consecutive positive integers is at most one. It is amazing, therefore, that we start analyzing when this happens.

The simplest sequence of \(k\) consecutive positive integers we can think of is the sequence

$$(1, 2, \ldots, k)$$

which sums to

$$\frac{k(k+1)}{2}$$

The simplest sequence but one of length \(k\) definitely is
