of consecutive elements in a list. For example, suppose we want to make a rule to replace a sum of squares of a sine and a cosine with 1, even if they are not consecutive in the sum:

```
(+ ... (expt (sin theta) 2) ... (expt (cos theta) 2) ...)
(+ i)
```

The ... may stand for many terms. We will use a segment variable, written with the prefix ??, to match many terms. So the pattern we will write:

```
(?? t1)
expt (sin ?? x) 2)
(?? t2)
expt (cos ?? x) 2)
(?? t3)
```

We need three segment variables here. The segment variable (?? t1) will match the terms before the sine term, (?? t2) will match the terms between the sine term and the cosine term, and (?? t3) will match the terms after the cosine term.

Segment variables have a profound effect, because we don't know how long a segment is until we find the next part that matches, and we may be able to match the same data item many ways. For example, there may be squares of both sines and cosines of two different angles in the same sum. Even simpler, the pattern

```
(a ?? x) (?? y) (?? x) c)
```

can match the datum

```
(a b b b b b c)
```

in four different ways.(Notice that the segment variable x must eat up the same number of bs in the two places it appears in the pattern.) So the matcher must do a search over the space of possible assignments to the segment variables.

# 4.2 Term rewriting