
First the program compares a[0] to a[1], then a[1] to a[2], then a[2] to a[3], and so on until it completes the pass by comparing a[8] to a[9]. Although there are 10 elements, only nine comparisons are performed. Because of the way the successive comparisons are made, a large value may move down the array many positions on a single pass, but a small value may move up only one position.

On the first pass, the largest value is guaranteed to sink to the bottom element of the array, a[9]. On the second pass, the second-largest value is guaranteed to sink to a[8]. On the ninth pass, the ninth-largest value sinks to a[1]. This leaves the smallest value in a[0], so only nine passes of the array are needed to sort the array, even though there are ten elements.

The sorting is performed by the nested for loops (lines 21–34). If a swap is necessary, it's performed by the three assignments

```
hold = a[i];
a[i] = a[i + 1];
a[i + 1] = hold;
```

where the extra variable hold temporarily stores one of the two values being swapped. The swap cannot be performed with only the two assignments

```
a[i] = a[i + 1];
a[i + 1] = a[i];
```

If, for example, a[i] is 7 and a[i + 1] is 5, after the first assignment both values will be 5 and the value 7 will be lost—hence the need for the extra variable hold.

The chief virtue of the bubble sort is that it's easy to program. However, it runs slowly because every exchange moves an element only one position closer to its final destination. This becomes apparent when sorting large arrays. In the exercises, we'll develop more efficient versions of the bubble sort. Far more efficient sorts than the bubble sort have been developed. We'll investigate other algorithms in Appendix D. More advanced courses investigate sorting and searching in greater depth.

## 6.9 Case Study: Computing Mean, Median and Mode Using Arrays

We now consider a larger example. Computers are commonly used for survey data analysis to compile and analyze the results of surveys and opinion polls. Figure 6.16 uses array response initialized with 99 responses to a survey. Each response is a number from 1 to 9. The program computes the mean, median and mode of the 99 values. Figure 6.17 contains a sample run of this program. This example includes most of the common manipulations usually required in array problems, including passing arrays to functions.

```
1 // Fig. 6.16: fig06_16.c
2 // Survey data analysis with arrays:
3 // computing the mean, median and mode of the data.
4 #include <stdio.h>
5 #define SIZE 99
```

Fig. 6.16 | Survey data analysis with arrays: computing the mean, median and mode of the data. (Part 1 of 4.)

```c
// function prototypes
void mean(const unsigned int answer[]);
void median(unsigned int answer[]);
void mode(unsigned int freq[], const unsigned int answer[]);
void bubbleSort(unsigned int a[]);
void printArray(const unsigned int a[]);

// function main begins program execution
int main(void)
{
    unsigned int frequency[10] = {0}; // initialize array frequency

    // initialize array response
    unsigned int response[SIZE] =
    {6, 7, 8, 9, 8, 7, 8, 9, 8, 9,
     7, 8, 9, 5, 9, 8, 7, 8, 7, 8,
     6, 7, 8, 9, 3, 9, 8, 7, 8, 7,
     7, 8, 9, 8, 9, 8, 9, 7, 8, 9,
     6, 7, 8, 7, 7, 9, 9, 8, 9, 2,
     7, 8, 9, 8, 9, 8, 9, 7, 5, 3,
     5, 6, 7, 2, 5, 3, 9, 4, 6, 4,
     7, 8, 9, 6, 8, 7, 8, 9, 7, 8,
     7, 4, 4, 2, 5, 3, 8, 7, 5, 6,
     4, 5, 6, 1, 6, 5, 7, 8, 7};

    // process responses
    mean(response);
    median(response);
    mode(frequency, response);
}

// calculate average of all response values
void mean(const unsigned int answer[])
{
    printf("\n\n\n\n%s\n%s\n%s\n", "********", " Mean", "********");
    unsigned int total = 0; // variable to hold sum of array elements

    // total response values
    for (size_t j = 0; j < SIZE; ++j) {
        total += answer[j];
    }

    printf("The mean is the average value of the data\n"
           "items. The mean is equal to the total of\n"
           "all the data items divided by the number\n"
           "of data items (%u). The mean value for\n"
           "this run is: %u / %u = %.4f\n\n",
           SIZE, total, SIZE, (double) total / SIZE);
}
```

57
58 // sort array and determine median element's value
59 void median(unsigned int answer[])
60 {
61     printf("\n%s\n%s\n%s\n", "**********", " Median ", "**********");
62     printf("The unsorted array of responses is\n");

63     printArray(answer); // output unsorted array

64     bubbleSort(answer); // sort array

65     printf("\n%s\n", "The sorted array is");
     printArray(answer); // output sorted array

     // display median element
     printf("\nThe median is element %u of\n"
            "the sorted %u element array.\n"
            "For this run the median is %u\n\n",
            SIZE / 2, SIZE, answer[SIZE / 2]);
}

78 // determine most frequent response
79 void mode(unsigned int freq[], const unsigned int answer[])
80 {
81     printf("\n%s\n%s\n%s\n", "**********", " Mode ", "**********");

     // initialize frequencies to 0
     for (size_t rating = 1; rating <= 9; ++rating) {
         freq[rating] = 0;
     }

     // summarize frequencies
     for (size_t j = 0; j < SIZE; ++j) {
         ++freq[answer[j]];
     }

     // output headers for result columns
     printf("%s %11s %19s\n", "Response", "Frequency", "Histogram");

     // output results
     unsigned int largest = 0; // represents largest frequency
     unsigned int modeValue = 0; // represents most frequent response

     for (rating = 1; rating <= 9; ++rating) {
         printf("%8u%11u", rating, freq[rating]);

Fig. 6.16 | Survey data analysis with arrays: computing the mean, median and mode of the data. (Part 3 of 4.)

```c
// keep track of mode value and largest frequency value
if (freq[rating] > largest) {
    largest = freq[rating];
    modeValue = rating;
}

// output histogram bar representing frequency value
for (unsigned int h = 1; h <= freq[rating]; ++h) {
    printf("%s", "*");
}

puts(""); // begin a new line of output
}

// display the mode value
printf("\nThe mode is the most frequent value.\n"
"For this run the mode is %u which occurred "
"%u times.\n", modeValue, largest);
}

// function that sorts an array with bubble sort algorithm
void bubbleSort(unsigned int a[])
{
    // loop to control number of passes
    for (unsigned int pass = 1; pass < SIZE; ++pass) {

        // loop to control number of comparisons per pass
        for (size_t j = 0; j < SIZE - 1; ++j) {

            // swap elements if out of order
            if (a[j] > a[j + 1]) {
                unsigned int hold = a[j];
                a[j] = a[j + 1];
                a[j + 1] = hold;
            }
        }
    }
}

// output array contents (20 values per row)
void printArray(const unsigned int a[])
{
    // output array contents
    for (size_t j = 0; j < SIZE; ++j) {

        if (j % 20 == 0) { // begin new line every 20 values
            puts("");
        }

        printf("%2u", a[j]);
    }
}
```

~~~text
**********
   Mean
**********
The mean is the average value of the data
items. The mean is equal to the total of
all the data items divided by the number
of data items (99). The mean value for
this run is: 681 / 99 = 6.8788

**********
  Median
**********
The unsorted array of responses is
6 7 8 7 8 9 8 7 9 8 7 9 8 7 8 7 8
6 7 8 9 3 9 8 7 8 7 8 8 9 8 7 9 8 9
6 7 8 7 8 7 9 8 9 2 7 8 9 8 9 7 5 3
5 6 7 2 5 3 9 4 6 4 7 8 9 6 8 7 8 7
7 4 4 2 5 3 8 7 5 6 4 5 6 1 6 5 7 8 7

The sorted array is
1 2 2 2 3 3 3 4 4 4 4 5 5 5 5 5 5 5
5 6 6 6 6 6 6 6 6 7 7 7 7 7 7 7 7 7 7
7 7 7 7 7 7 7 7 7 7 7 7 8 8 8 8 8 8
8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8
9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9

The median is element 49 of
the sorted 99 element array.
For this run the median is 7

**********
   Mode
**********
Response  Frequency            Histogram

                                    1   1   2   2
                                5   0   5   0   5
1       1       *
2       3       ***
3       4       ****
4       5       *****
5       8       ********
6       9       *********
7       23      ***********************
8       27      ***************************
9       19      *******************

The mode is the most frequent value.
For this run the mode is 8 which occurred 27 times.
~~~

Fig. 6.17 | Sample run for the survey data analysis program.
