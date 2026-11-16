+   Exercise 101 Do the following:
+   (a) Use the techniques given in Exercise 100 to prove that \( A_2(8, 4, 5) \le 8 \).
+   (b) Show that \( A_2(8, 4, 5) = 8 \). Hint: By Exercise 100, \( A_2(8, 4, 5) = A_2(8, 4, 3) \). A binary \( (8, 4, 4) \) code with all codewords of weight 3 exists where, for each coordinate, there are exactly three codewords with a 1 in that coordinate.

# 2.3.3 The Johnson Bound for \( A_q(n, d) \)

The bounds on \( A_q(n, d, w) \) can be used to give upper bounds on \( A_q(n, d) \) also due to Johnson [159]. As can be seen from the proof, these bounds strengthen the Sphere Packing Bound. The idea of the proof is to count not only the vectors in \( \mathbb{F}_q^n \) that are within distance \( t = \lfloor (d-1)/2 \rfloor \) of all codewords (that is, the disjoint spheres of radius \( t \) centered at codewords) but also the vectors at distance \( t+1 \) from codewords that are not within these spheres. To accomplish this we need the following notation. If \( \mathcal{C} \) is a code of length \( n \) over \( \mathbb{F}_q \) and \( \mathbf{x} \in \mathbb{F}_q^n \), let \( d(\mathcal{C}, \mathbf{x}) \) denote the distance from \( \mathbf{x} \) to \( \mathcal{C} \). So \( d(\mathcal{C}, \mathbf{x}) = \min\{d(\mathbf{c}, \mathbf{x}) \mid \mathbf{c} \in \mathcal{C}\} \).

# Theorem 2.3.8 (Johnson Bound for \( A_q(n, d) \)) Let \( t = \lfloor (d-1)/2 \rfloor \).

+   (i) If \( d \) is odd, then
+   \( A_q(n, d) \le \frac{q^n}{\sum_{i=0}^t \binom{n}{i}(q-1)^i + \frac{\binom{n}{t+1}(q-1)^{t+1}}{\binom{t+1}{t} - \left(\frac{d}{t}\right)} A_q(n, d, d)} \).

+   (ii) If \( d \) is even, then
+   \( A_q(n, d) \le \frac{q^n}{\sum_{i=0}^t \binom{n}{i}(q-1)^i + \frac{\binom{n}{t+1}(q-1)^{t+1}}{A_q(n, d, t+1)}} \).

+   (iii) If \( d \) is odd, then
+   \( A_2(n, d) \le \frac{2^n}{\sum_{i=0}^t \binom{n}{i} + \frac{\binom{n}{t+1} - \binom{d}{t} A_2(n, d, d)}{\lfloor \frac{n}{t+1} \rfloor}} \).

+   (iv) If \( d \) is even, then
+   \( A_2(n, d) \le \frac{2^n}{\sum_{i=0}^t \binom{n}{i} + \left\lfloor \frac{n}{t+1} \right\rfloor} \). (2.12)