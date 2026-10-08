![](bbox=[0.34, 0.05, 0.68, 0.13])

Figure 5.7: The bow h in the arc and the noise level \( \sigma \).

illustrated in Fig. 5.7. Here

```
\begin{equation}
h=R(1-\cos \alpha / 2)
\end{equation}
```

is a crucial parameters, the distance from the midpoint of the arc to its chord ($h$ is called the “bow” in the arc [90]). If the noise level is smaller than the bow ($\sigma<h$), then the shape of the arc is “well defined” [90], i.e., recognizable, and circle fitting algorithms have a chance to succeed (and some do). On the other hand, if $\sigma>h$, then the noise completely blurs the arc, and circle fitting procedures consistently fail to find it. In our experiment, $R=1$ and $\sigma=0.05$, hence the critical arc size is

```
\begin{equation}
\alpha_{\mathrm{cr}}=2 \cos ^{-1}(1-\sigma / R)=36^{\circ}
\end{equation}
```

below which everybody collapses. Of course, reducing the noise level $\sigma$ would allow our algorithms to perform well on smaller arcs. Generally, the fitting algorithms can handle arbitrarily small arcs, as long as $\sigma$ does not exceed the bow.

**Some other algebraic fits.** We only describe here the most popular algebraic fitting schemes, but a few others are worth mentioning. Gander, Golub, and Strebøl [67] propose to minimize the same function (5.38) that we used for the Pratt and Kåsa methods, but subject to a more straightforward constraint $\|\mathbf{A}\|=1$, i.e.,

```
\begin{equation}
A^{2}+B^{2}+C^{2}+D^{2}=1 .
\end{equation}
```

Our analysis in Section 5.7 shows, however, that the resulting fit would not be invariant under translations; in fact the authors [67] also admit that it is geometrically “unsatisfactory.”

Nievergelt [137] proposes a fairly complicated algebraic fit, but if one inspects it closely, it turns out to be equivalent to the minimization of the same function (5.38) subject to the constraint

```
\begin{equation}
A^{2}+B^{2}+C^{2}=1 .
\end{equation}
```

Nievergelt argues that his fit handles certain singular cases (namely, those of collinear data) better than the Kåsa fit does. Nievergelt also recognizes that his fit would not be invariant under translations. As a remedy he uses a prior