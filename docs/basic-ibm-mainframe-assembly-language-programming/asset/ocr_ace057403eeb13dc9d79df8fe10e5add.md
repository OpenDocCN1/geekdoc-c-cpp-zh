```
34 LA R2,1(0,R2)
35 C R2,=F'10'
36 BL FLOOP
37 SUBEXIT
38 *
39 * TABLE OF NUMBERS TO SORT
40 *
41 TAB DC F'9'
42 DC F'7'
43 DC F'3'
44 DC F'10'
45 DC F'4'
46 DC F'1'
47 DC F'2'
48 DC F'11'
49 DC F'5'
50 DC F'0'
51
52 OUT DS CL12
53
54 END
```

Figure 87 Bubble Sort

# 23.5 Bubble Sort

The program in Figure 87 performs a bubble sort on the table of ten full word binary numbers beginning at label TAB. The program consists of two loops: an outer loop beginning at OUTER and an inner loop beginning at LOOP.

The inner loop examines each entry of the table from positions 0 to 9 and compares each with the entry in the position above it. That is, the entry at position 0 is compared with the entry at position 1, entry 1 is compared with entry 2 and so forth until entry 9 is compared with entry 10.