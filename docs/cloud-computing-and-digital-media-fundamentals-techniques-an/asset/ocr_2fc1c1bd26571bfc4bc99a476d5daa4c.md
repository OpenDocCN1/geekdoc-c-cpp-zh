# GPU and Cloud Computing for Music Information Retrieval ■ 87

Frame s(i):

![](bbox=[0.378, 0.098, 0.796, 0.213])

Shifted frame s(i + τ):

τ = 30 acf(30) = inner product of overlap length

Pitch period

```
acf(τ) = \sum_{i=0}^{n-1-τ} s(i)s(i+τ)
```

![](bbox=[0.406, 0.243, 0.703, 0.003313])

Figure 4.4 ACF operation.

# 4.3.2 Linear Scaling

The tempo of a user's singing or humming is usually different from that of the intended song in the database. Thus, the QBSH system needs to compress or stretch pitch vector to match the song in the database. Assuming that the query input is d-second long, we can compress or stretch the original vector to obtain r different versions, with their lengths equally spaced between sf_{min} and sf_{max} which are the minimum and maximum of the scaling factor, respectively, 0 < sf_{min} < 1 < sf_{max} . The distance between the input pitch vector and a particular song is then the minimum of the r distances between the r vectors and that song, as shown in Figure 4.5, where we compress/stretch the d-second vector to obtain five vectors with lengths equally spaced between 0.5 × d and 1.5 × d. The best result is obtained when the scaling factor is 1.25.

The user's singing/humming also differs from the target song in terms of key. Key transposition can be simply handled by shifting the mean (if L2-norm is used) or the median (if L1-norm is used) of the query input and a database song (of the same length). The distance is usually based on L<sub>p</sub>norm, defined as:

```
|x_1 - y_1|_p = (\hat{\mathbb{E}}_1 |x_1 - y_1|^p)^{1/p}
```

where:
x and y are two vectors of the same length

Figure 4.6 shows a typical example of LS using the L1- and L2-norms.