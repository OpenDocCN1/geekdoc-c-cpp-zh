```
Pattern 3: f~2, f~3, f~4, f~5, f~6, f~7, f~8
Pattern 4: f~2, f~3, f~4, f~5, f~6, f~7, f~8
Pattern 5: f~2, f~3, f~4, f~5, f~6, f~7, f~8
```

Rule match-1 has the following partial matches:

```
Pattern 1: [f~1]
Patterns 1~2: [f~1, f~2]
Patterns 1~3: [f~1, f~2, f~4]
Patterns 1~4: [f~1, f~2, f~4, f~6]
Patterns 1~5: [f~1, f~2, f~4, f~6, f~8]
```

In total rule match-1 has 29 pattern matches and 5 partial matches.

# Counting for Rule match-2

Rule match-2 has the following pattern matches:

```
Pattern 1: f~2, f~3, f~4, f~5, f~6, f~7, f~8
Pattern 2: f~2, f~3, f~4, f~5, f~6, f~7, f~8
Pattern 3: f~2, f~3, f~4, f~5, f~6, f~7, f~8
Pattern 4: f~2, f~3, f~4, f~5, f~6, f~7, f~8
Pattern 5: f~1
```

Rules match-1 and match-2 have the same number of pattern matches. Now consider only the partial matches for pattern 1:

```
[f~2], [f~3], [f~4], [f~5], [f~6], [f~7], [f~8]
```

Pattern 1 has seven partial matches. This is no surprise since the partial and pattern matches will be the same for the first pattern. The partial matches for patterns 1 and 2, however, are numerous:

```
[f~2, f~2], [f~2, f~3], [f~2, f~4], [f~2, f~5],
[f~2, f~6], [f~2, f~7], [f~2, f~8],
[f~3, f~2], [f~3, f~3], [f~3, f~4], [f~3, f~5],
[f~3, f~6], [f~3, f~7], [f~3, f~8],
[f~4, f~2], [f~4, f~3], [f~4, f~4], [f~4, f~5],
[f~4, f~6], [f~4, f~7], [f~4, f~8],
[f~5, f~2], [f~5, f~3], [f~5, f~4], [f~5, f~5],
[f~5, f~6], [f~5, f~7], [f~5, f~8],
[f~6, f~2], [f~6, f~3], [f~6, f~4], [f~6, f~5],
[f~6, f~6], [f~6, f~7], [f~6, f~8],
[f~7, f~2], [f~7, f~3], [f~7, f~4], [f~7, f~5],
[f~7, f~6], [f~7, f~7], [f~7, f~8],
[f~8, f~2], [f~8, f~3], [f~8, f~4], [f~8, f~5],
[f~8, f~6], [f~8, f~7], [f~8, f~8]
```