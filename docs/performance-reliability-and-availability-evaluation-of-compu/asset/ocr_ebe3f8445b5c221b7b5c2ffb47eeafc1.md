# RAID 1

| A1 | A2 | A3 | Ap1 |
|---|---|---|---|
| A4 | A5 | Ap2 | A6 |
| A7 | Ap3 | A8 | A9 |
| Ap4 | A10 | A11 | A12 |
| A13 | A14 | A15 |

| A1 | A2 | A3 | Ap1 |
|---|---|---|---|
| A4 | A5 | Ap2 | A6 |
| A7 | Ap3 | A8 | A9 |
| Ap4 | A10 | A11 | A12 |
| A13 | A14 | A15 | Ap5

(a) RAID 51

# RAID 0

| A1 | A2 | A3 | Ap11 |
|---|---|---|---|
| A6 | A7 | Ap12 | A8 |
| A12 | Ap13 | A13 | A14 |
| Ap14 | A18 | A19 | A20 |
| A24 | A25 | A26 | Ap15

| A4 | A5 | A6 | Ap21 |
|---|---|---|---|
| A9 | A10 | Ap22 | A11 |
| A15 | Ap23 | A16 | A17 |
| Ap24 | A21 | A22 | A23 |
| A27 | A28 | A29 | Ap25

(b) RAID 50

**Figure 17.14** RAID 51 (a) and RAID 50 (b)

details, see Chapter 18. The storage capacity efficiency is specified by

$SCE = \frac{ESC}{TDC} \frac{(n-4)}{n}, \quad (17.1.7)$

where $ESC = (n-4) \times DC$.

**RAID 61** is implemented by mirroring (RAID 1) in an entire RAID 6 array. RAID 61 requires at least eight disks and tolerates to four disk failures (see Figure 17.14.b). The storage capacity efficiency is specified by

$SCE = \frac{ESC}{TDC} \frac{(n-4)/2}{n}, \quad (17.1.8)$

where $ESC = ((n-4)/2) \times DC$.