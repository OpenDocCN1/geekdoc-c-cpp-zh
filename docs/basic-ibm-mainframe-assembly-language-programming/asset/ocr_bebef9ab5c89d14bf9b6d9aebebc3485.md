```
88 *
89 * TRT TABLE TO CONVERT TO UPPER CASE AND REMOVE NON-ALPHAS
90 *
91 TRTAB DC 256C' '
92 ORG TRTAB+C'a'
93 DC C'ABCDEFGH I'
94 ORG TRTAB+C'A'
95 DC C'ABCDEFGH I'
96
97 ORG TRTAB+C'j'
98 DC C'JKLMNOPQR'
99 ORG TRTAB+C'J'
100 DC C'JKLMNOPQR'
101
102 ORG TRTAB+C's'
103 DC C'STUVWXYZ'
104 ORG TRTAB+C'S'
105 DC C'STUVWXYZ'
106
107 ORG TRTAB+C'-' * RETAIN HYP HENS
108 DC C'-'
109
110 ORG TRTAB+C'!' * RETAIN SINGLE QUOTES
111 DC C'\'\''
112 ORG
113
114 LTORG * LITERALS NEED TO BE PRIOR TO TABLE
115
116 DS 0F * FULL WORD ALIGN
117 *
118 * TABLE IS 1000 ENTRIES, EACH ENTRY IS 8 CHARS FOR WORD
119 * AND 4 BYTES COUNT.
120 *
121 TAB DS 12000C
122 END HEX
```

Figure 91 Word Count Program

# 23.10 Word Count Program with DSECT

The previous program works but it doesn't deal with the word/count data structure very intelligently. Instead, it handles these as numeric displacements relative to a register as in lines 68 through 72. Line 68 copies the word from a node pointed to by R5 to an output field and then lines 69 and 70 load the count (8 bytes displaced from the word) into R7, convert it to printable decimal, and store it in the last 12 bytes of the output field. Even