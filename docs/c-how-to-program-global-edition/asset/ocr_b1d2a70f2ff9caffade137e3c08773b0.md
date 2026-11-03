```
60
61 // if searchKey is greater than middle element, set new low
62 else {
63 low = middle + 1; // search high end of array
64 }
65 } // end while
66
67 return -1; // searchKey not found
68 }
69
70 // Print a header for the output
71 void printHeader(void)
72 {
73 puts("\nIndices:");
74
75 // output column head
76 for (unsigned int i = 0; i < SIZE; ++i) {
77 printf("%3u ", i);
78 }
79
80 puts("");
81 // start new line of output
82 // output line of - characters
83 for (unsigned int i = 1; i <= 4 * SIZE; ++i) {
84 printf("%s", "-");
85 }
86
87 puts("");
88 // start new line of output
89 }
90 // Print one row of output showing the current
91 // part of the array being processed.
92 void printRow(const int b[], size_t low, size_t mid, size_t high)
93 {
94 // loop through entire array
95 for (size_t i = 0; i < SIZE; ++i) {
96
97 // display spaces if outside current subarray range
98 if (i < low || i > high) {
99 printf("%s", " ");
100 }
101 else if (i == mid) { // display middle element
102 printf("%3d*", b[i]); // mark middle value
103 }
104 else { // display other elements in subarray
105 printf("%3d ", b[i]);
106 }
107 }
108
109 puts(""); // start new line of output
110 }
```