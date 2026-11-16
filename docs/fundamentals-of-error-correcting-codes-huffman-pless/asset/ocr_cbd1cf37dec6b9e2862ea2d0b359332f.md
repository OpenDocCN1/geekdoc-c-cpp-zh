+   (i) \( a_i(x)f(x) + b_i(x)s(x) = r_i(x) \) for \( i \ge -1 \).
+   (ii) \( b_i(x)r_{i-1}(x) - b_{i-1}(x)r_i(x) = (-1)^i f(x) \) for \( i \ge 0 \).
+   (iii) \( a_i(x)b_{i-1}(x) - a_{i-1}(x)b_i(x) = (-1)^{i+1} \) for \( i \ge 0 \).
+   (iv) \( \deg b_i(x) + \deg r_{i-1}(x) = \deg f(x) \) for \( i \ge 0 \).

Proof: All of these are proved by induction. For (i), the cases \( i = -1 \) and \( i = 0 \) follow directly from the initial values set in Step I of the Sugiyama Algorithm and the values \( a_{-1}(x) = 1 \) and \( a_0(x) = 0 \). Assuming (i) holds with \( i \) replaced by \( i - 1 \) and \( i - 2 \), we have

```
\begin{align*}
a_i(x)f(x) + b_i(x)s(x) &= [a_{i-2}(x) - h_i(x)a_{i-1}(x)]f(x) \\
&+ [b_{i-2}(x) - h_i(x)b_{i-1}(x)]s(x) \\
&= a_{i-2}(x)f(x) + b_{i-2}(x)s(x) \\
&- h_i(x)[a_{i-1}(x)f(x) + b_{i-1}(x)s(x)] \\
&= r_{i-2}(x) - h_i(x)r_{i-1}(x) = r_i(x),
\end{align*}
```

completing (i).

Again when \( i = 0 \), (ii) follows from Step I of the Sugiyama Algorithm. Assume (ii) holds with \( i \) replaced by \( i - 1 \). Then

```
\begin{align*}
b_i(x)r_{i-1}(x) - b_{i-1}(x)r_i(x) &= [b_{i-2}(x) - h_i(x)b_{i-1}(x)]r_{i-1}(x) - b_{i-1}(x)r_i(x) \\
&= b_{i-2}(x)r_{i-1}(x) - b_{i-1}(x)[h_i(x)r_{i-1}(x) + r_i(x)] \\
&= b_{i-2}(x)r_{i-1}(x) - b_{i-1}(x)r_{i-2}(x) \\
&= -(-1)^{i-1} f(x) = (-1)^i f(x),
\end{align*}
```

verifying (ii).

When \( i = 0 \), (iii) follows from Step I of the Sugiyama Algorithm, \( a_{-1}(x) = 1 \), and \( a_0(x) = 0 \). Assume (iii) holds with \( i \) replaced by \( i - 1 \). Then

```
\begin{align*}
a_i(x)b_{i-1}(x) - a_{i-1}(x)b_i(x) &= [a_{i-2}(x) - h_i(x)a_{i-1}(x)]b_{i-1}(x) \\
&- a_{i-1}(x)[b_{i-2}(x) - h_i(x)b_{i-1}(x)] \\
&= -[a_{i-1}(x)b_{i-2}(x) - a_{i-2}(x)b_{i-1}(x)] \\
&= -(-1)^i = (-1)^{i+1},
\end{align*}
```

proving (iii).

When \( i = 0 \), (iv) follows again from Step I of the Sugiyama Algorithm. Assume (iv) holds with \( i \) replaced by \( i - 1 \), that is, \( \deg b_{i-1}(x) + \deg r_{i-2}(x) = \deg f(x) \). In Step II of the Sugiyama Algorithm, we have \( \deg r_i(x) < \deg r_{i-2}(x) \). So \( \deg b_{i-1}(x)r_i(x) = \deg b_{i-1}(x) + \deg r_i(x) < \deg f(x) \) implying (iv) for case \( i \) using part (ii).

We now verify that the Sugiyama Algorithm works. By Lemma 5.4.11(i) we have
\( a_i(x)x^{2t} + b_i(x)S(x) = r_i(x). \) (5.13)

From the key equation, we also know that
\( a(x)x^{2t} + \sigma(x)S(x) = \omega(x) \) (5.14)