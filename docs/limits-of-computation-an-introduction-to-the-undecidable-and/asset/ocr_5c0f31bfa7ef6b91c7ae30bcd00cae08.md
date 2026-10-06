Left moves: These are more complex since the state will move to the left across whatever symbol was there. Thus, if q reading $\sigma$ moves left, writes $	au$, and goes to state p, then for every symbol $v$ in the tape alphabet, add

```
$vq\sigma$
np\tau$$
```

Extending a configuration left and right of head: These are simple but necessary. For every $\sigma$ in $\Gamma$, add

```
$\sigma$
$\sigma$
```

Also add

```
$#$
#$
```

Extending a configuration to new areas of tape: For each state $q$ in $Q$, add

```
$q#$ and $#q$
qB#$ $\#Bq$
```

These moves allow the string to expand to the left and right if the head reaches the markers #. These begin marking the start and end of the input string. They continue to mark either the start/end of input or the furthest left/right that the head has reached so far during its computation.

Now, notice that each string keeps the top and bottom strings so far equal in length, or lengthens the bottom string. The next tiles or pairs of strings are the only ones that are longer than top on the bottom.

Finishing up from accept state: Add

```
$Q_{accept}###$ (top length = 4, bottom length = 1)
#$
```