![](bbox=[0.22, 0.08, 0.72, 0.44])

Figure 4.11 Normalized bar graph from R of age_binned with response overlay.

| | under 27 | 27 to 60 | Over 60 | total |
|---|---|---|---|---|
| no | 1255 | 22315 | 316 | 23886 |
| yes | 322 | 2399 | 267 | 2988 |
| total | 1377 | 24714 | 583 | 26674 |

Figure 4.12 Contingency table from R of age_binned and response.

| | under 27 | to 60 | over 60 |
|---|---|---|---|
| no | 79.6 | 90.3 | 54.2 |
| yes | 20.4 | 9.7 | 45.8 |

Figure 4.13 Contingency table from R of age_binned and response with column percentages.

Bin the values using cut() from the pandas package.

```
```python
bank_train['age_binned'] = pd.cut(x = bank_train['age'],
                                  bins = [0, 27, 60.01, 100],
                                  labels=["Under 27", "27 to 60", "Over 60"], right =
                                  False)
```
```

The x = input specifies the variable that you want to divide into categories. The bins = input specifies the edges of each bin. The labels = input specifies the bin label. The right = False input specifies that we want our bins to exclude the right-hand cutpoint. For example, the first bin will include all ages from 0 up to (but