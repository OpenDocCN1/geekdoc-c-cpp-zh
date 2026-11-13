Now, backtrack on P and compare P[1] and S[3].

**Step 4:** Here, i = 4, q = 0; comparing P[1] with S[4], we notice that P[1] does not match with S[4].

| S | b | a | c | b | a | a | b | a | b | a | b | a | c | a | a | b |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| P | | | | a | b | a | b | a | c | a | | | | | | | |

**Step 5:** Currently, i = 5, q = 0; comparing P[1] with S[5], we notice that P[1] matches with S[5].

| S | b | a | c | b | a | b | a | b | a | b | a | b | a | c | a | a | b |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| P | | | | | a | b | a | b | a | c | a | | | | | | | |

**Step 6:** For i = 6, q = 1, we compare P[2] with S[6]. We see that P[2] matches with S[6].

| S | b | a | c | b | a | b | b | a | b | a | b | a | b | a | c | a | a | b |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| P | | | | | | a | b | a | b | a | c | a | | | | | | | |

**Step 7:** For i = 7, q = 2, we compare P[3] with S[7], and we see that P[3] matches with S[7].

| S | b | a | c | b | a | b | a | b | a | b | a | b | a | c | a | a | b |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| P | | | | | | | a | b | a | b | a | c | a | | | | | | |

**Step 8:** With i = 8, q = 3, and when P[4] and S[8] are compared, it results in P[4] matching with S[9].