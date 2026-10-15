This data set is concatenated with the following data set:

| Observation ID | Variable 1 | Variable 2 | Variable 3 |
|---|---|---|---|
| 8 |  |  |  |
| 9 |  |  |  |
| 10 |  |  |  |
| 11 |  |  |  |
| 12 |  |  |  |

The following data set is produced:

| Observation ID | Variable 1 | Variable 2 | Variable 3 |
|---|---|---|---|
| 1 |  |  |  |
| 2 |  |  |  |
| 3 |  |  |  |
| 4 |  |  |  |
| 5 |  |  |  |
| 6 |  |  |  |
| 7 |  |  |  |
| 8 |  |  |  |
| 9 |  |  |  |
| 10 |  |  |  |
| 11 |  |  |  |
| 12 |  |  |  |

Suppose you (foolishly? unnecessarily?) read the nit rofen data into a separate data set for each concentration. In Display 2.23, the total brood count variable is entered into separate data sets, one for each concentration condition. A new variable is defined for each concentration, and then each concentration-specific data set is combined to create a single analysis data set using the SET command.

```
data set_all5;
    set conc_0 conc_80 conc_160 conc_235 conc_310;
```