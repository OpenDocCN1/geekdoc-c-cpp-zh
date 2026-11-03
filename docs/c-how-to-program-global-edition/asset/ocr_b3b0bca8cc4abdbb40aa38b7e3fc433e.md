```
57
58 // sort array and determine median element's value
59 void median(unsigned int answer[])
60 {
61     printf("\n%s\n%s\n%s", "**********", " Median ", "**********",
62            "The unsorted array of responses is");
63
64     printArray(answer); // output unsorted array
65
66     bubbleSort(answer); // sort array
67
68     printf("\n", "\nThe sorted array is");
69     printArray(answer); // output sorted array
70
71     // display median element
72     printf("\nThe median is element %u of\n"
73            "the sorted %u element array.\n"
74            "For this run the median is %u\n\n",
75            SIZE / 2, SIZE, answer[SIZE / 2]);
76 }
77
78 // determine most frequent response
79 void mode(unsigned int freq[], const unsigned int answer[])
80 {
81     printf("\n%s\n%s\n%s", "**********", " Mode ", "**********");
82
83     // initialize frequencies to 0
84     for (size_t rating = 1; rating <= 9; ++rating) {
85         freq[rating] = 0;
86     }
87
88     // summarize frequencies
89     for (size_t j = 0; j < SIZE; ++j) {
90         ++freq[answer[j]];
91     }
92
93     // output headers for result columns
94     printf("%s11s19s(\n%s54s\n%s54s\n\n",
95            "Response", "Frequency", "Histogram",
96            "1    2    2    5    0    5    0    5");
97
98     // output results
99     unsigned int largest = 0; // represents largest frequency
100    unsigned int modeValue = 0; // represents most frequent response
101
102    for (rating = 1; rating <= 9; ++rating) {
103        printf("%8u%11u", rating, freq[rating]);
```

Fig. 6.16 | Survey data analysis with arrays: computing the mean, median and mode of the data. (Part 3 of 4.)