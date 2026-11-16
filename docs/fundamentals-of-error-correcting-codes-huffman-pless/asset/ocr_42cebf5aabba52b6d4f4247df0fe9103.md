![](bbox=[0.15, 0.08, 0.85, 0.3])

Figure 14.3 Trellis for the encoder \( G_1 = [1 + D + D^2 \ 1 + D^2] \).

**Exercise 809** Verify that the edge labels for the four edges described in Example 14.2.4 are as claimed. \(\diamond\)

**Exercise 810** Give the state diagram for the encoder \( G'_2 \) of the (4, 2) convolutional code \( C_2 \) from Example 14.1.1. It may be easiest to draw the diagram in the form similar to that given in Figure 14.2(b). \(\diamond\)

**Exercise 811** Repeat Exercise 810 with the encoder \( G''_2 \) from Example 14.1.1. \(\diamond\)

# ## 14.2.2 Trellis diagrams

The trellis diagram for an encoding of a convolutional code is merely an extension of the state diagram starting at time \( i = 0 \). We illustrate this in Figure 14.3 for the generator matrix \( G_1 \) of the (2, 1) convolutional code \( C_1 \) from Example 14.1.1. The states are labeled \( a = 00 \), \( b = 01 \), \( c = 10 \), and \( d = 11 \). Notice that the trellis is a repetition of Figure 14.2(b) with the understanding that at time \( i = 0 \), the only state used is the zero state \( a \); hence at time \( i = 1 \), the only states that can be reached at time \( i = 1 \) are \( a \) and \( c \) and thus they are the only ones drawn at that time. Encoding can be accomplished by tracing left-to-right through the trellis beginning at state \( a \) (and ending at the zero state \( a \)). For instance, if we let state \( s \in \{a, b, c, d\} \) at time \( i \) be denoted by \( s_i \), then the encoding of 1011 is accomplished by the path \( a_0 b_1 c_2 d_3 b_4 s_5 \) by following a dashed, then solid, then two dashed, and finally two solid edges (as we must input two additional 0s to reach state \( a \)); this yields the codeword 111000101011 by writing down the labels on the edges of the path.

**Exercise 812** Use the trellis of Figure 14.3 to encode the following messages:
(a) 1001,
(b) 0011. \(\diamond\)

**Exercise 813** Draw the trellis diagram for the encoder \( G'_1 \) of the (2, 1) convolutional code \( C_1 \) presented in Example 14.1.1. The results of Exercise 808 will be useful. \(\diamond\)

**Exercise 814** Draw the trellis diagram for the encoder \( G'_2 \) of the (4, 2) convolutional code \( C_2 \) presented in Example 14.1.1. The results of Exercise 810 will be useful. \(\diamond\)