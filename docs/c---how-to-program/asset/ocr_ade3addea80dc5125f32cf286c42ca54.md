```
106 // keep track of mode value and largest frequency value
107 if (freq[rating] > largest) {
108     largest = freq[rating];
109     modeValue = rating;
110 }
111
112 // output histogram bar representing frequency value
113 for (unsigned int h = 1; h <= freq[rating]; ++h) {
114     printf("%s", "*");
115 }
116
117 puts(""); // being new line of output
118 }
119
120 // display the mode value
121 printf("\nThe mode is the most frequent value.\n"
122 "For this run the mode is %u which occurred"
123 " %u times.\n", modeValue, largest);
124 }
125
126 // function that sorts an array with bubble sort algorithm
127 void bubbleSort(unsigned int a[])
128 {
129     // loop to control number of passes
130     for (unsigned int pass = 1; pass < SIZE; ++pass) {
131
132         // loop to control number of comparisons per pass
133         for (size_t j = 0; j < SIZE - 1; ++j) {
134
135             // swap elements if out of order
136             if (a[j] > a[j + 1]) {
137                 unsigned int hold = a[j];
138                 a[j] = a[j + 1];
139                 a[j + 1] = hold;
140             }
141         }
142     }
143 }
144
145 // output array contents (20 values per row)
146 void printArray(const unsigned int a[])
147 {
148     // output array contents
149     for (size_t j = 0; j < SIZE; ++j) {
150
151         if (j % 20 == 0) { // begin new line every 20 values
152             puts("");
153         }
154
155
156         printf("%2u", a[j]);
157     }
}
```