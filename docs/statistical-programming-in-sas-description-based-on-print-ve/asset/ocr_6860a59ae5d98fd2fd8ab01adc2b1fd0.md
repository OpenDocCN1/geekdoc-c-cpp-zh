```
```sas
proc freq data=nitro_tox;
  table conc*cbrood3 / noperct nocol chisq trend exact;
run;
```
```

# **Display 3.24** Contingency table displaying nitrogen concentration and whether any young are produced in the third brood

The FREQ Procedure

Table of conc by cbrood3

conc (Nitrofen concentration)

| Frequency / Row Pct | none | some | Total |
|---|---:|---:|---:|
| 0 | 0<br>0.00 | 10<br>100.00 | 10 |
| 80 | 0<br>0.00 | 10<br>100.00 | 10 |
| 160 | 0<br>0.00 | 10<br>100.00 | 10 |
| 235 | 1<br>10.00 | 9<br>90.00 | 10 |
| 310 | 10<br>100.00 | 0<br>0.00 | 10 |
| Total | 11 | 39 | 50 |

*(continued)*