# Binary Search Program in C

Binary search is a fast search algorithm with runtime complexity of O(log n). This search algorithm works on the principle of divide and conquer. For this algorithm to work properly, the data collection should be in a sorted form.

# Implementation in C

```
#include <stdio.h>
#define MAX 20
// array of items on which linear search will be conducted. int intArray[MAX] =
{1,2,3,4,6,7,9,11,12,14,15,16,17,19,33,34,43,45,55,66};
void printline(int count){ int i;
for(i= 0;i<count-1;i++){ printf("=");
}
printf("=\n"); }
int find(int data){
int lowerBound = 0; int upperBound = MAX -1; int midPoint = -1;
int comparisons = 0; int index = -1;
while(lowerBound <= upperBound){
printf("Comparison %d\n" , (comparisons +1) ) ; printf("lowerBound : %d, intArray[%d]
= %d\n",lowerBound,lowerBound,intArray[lowerBound]);
lowerBound,lowerBound,intArray[lowerBound]); printf("upperBound : %d, intArray[%d]
= %d\n", upperBound,upperBound,intArray[upperBound]);
comparisons++;
// compute the mid point
// midPoint = (lowerBound + upperBound) / 2; midPoint = lowerBound + (upperBound -
lowerBound) / 2;
// data found
if(intArray[midPoint] == data){
index = midPoint;
break;
} else {
// if data is larger
if(intArray[midPoint] < data){
// data is in upper half
lowerBound = midPoint + 1;
}
// data is smaller
else{
// data is in lower half
upperBound = midPoint - 1;
}
}
}
```