
int searchArray(int x[], int n)
{
int lcv; //LOOP CONTROL VARIABLE USED TO ACCESS ARRAY ELEMENTS
int index = NOTFOUNDERROR; //VALUE TO RETURN WHICH INDICATES LOCATION OR NOT FOUND
for(lcv = 0; lcv < ARRAYSIZE; lcv++)
{
if(x[lcv] == n)
{
index = lcv;
lcv = ARRAYSIZE;
}
}
return(index);
}

The user-defined searching function above will search every element of the array until one of the following events takes place:

- The target is found, the loop terminates, and the index value is returned.
- The end of the array is reached, the loop terminates, and the "not found" value is returned.

int getTarget(void)
{
int target;
do
{
printf("Please enter the target value: ");
scanf("%d", &target);
if(target < 0)
printf("Please enter a valid target value >= 0!\n");
}while(target < 0);
return(target);
}

This type of search is known as the **sequential search** because each element of the array may potentially be referenced in order to find the desired element or to determine that element does not exist.

What is the goodness of the **sequential searching** algorithm?

- It works! It is simple.

What problems are associated with the use of the sequential searching algorithm?

| Question | Answer |
|---|---|
| What if we had a very large data set and the value we are looking for does not exist? | It would take a long time to search every element and make this determination. |
| What if multiple instances of the target value are potentially present in the array? | The entire array must now be searched to find every instance of a target in an unsorted array. |

## The Binary Search

- It is possible to reduce the time (both average and worst-case) it takes to complete a search by using an alternative searching algorithm known as the **binary search**. The binary search does require that the **data in the array be sorted**.

| Question | Answer |
|---|---|
| Is there a cost associated with sorting data? | Yes, but if we search our data frequently it is worth paying the cost of sorting and maintaining our data in a sorted state. |
| Should the binary search always be used when searching? | No, only when the data set is large and searched frequently. |

## New Integer Variables in the Binary Search

- **first** – This integer will represent the lowest index value at which the target value may potentially be found in the array.
- **last** – This integer will represent the highest index value at which the target value may potentially be found in the array.
- **mid** – The average of the **first** and **last** variables will determine where in the array the next comparison will be made with the target value. The **mid** is updated at the start of every iteration of the binary search process.
- How and when are the **first** and **last** variables updated? When the value at the **mid** is less than the target then the **first** is set to the value of the **mid** plus one. When the value at the **mid** is greater than the target then the **last** is set to the value of the **mid** minus one.

## Binary Search Example

Assume we have the array given below, notice it is sorted and will remain sorted throughout the entire algorithm. A searching algorithm should never alter the data it searches! Target = 25.

| 3 | 5 | 6 | 10 | 12 | 15 | 17 | 18 | 21 | 22 | 25 | 27 | 30 | 31 | 33 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |

What is the goodness of the binary search as applied to the example above?

- Only four comparisons were needed to find target (in the above example). A sequential search would have required 11.
- Bigger Point: With each comparison made between the target and the element at the midpoint we eliminate approximately half (hence the name binary) of the remaining index values as a possible location where the target could be found.

How does the binary search compare with the sequential search when it comes to finding a value that is not present in the array?

- The sequential search requires EVERY element of the array to be searched to be sure that the value does not exist.

Let's see in the example below how the binary search deals with a value that does not exist! Target = 14.

| 3 | 5 | 6 | 10 | 12 | 15 | 17 | 18 | 21 | 22 | 25 | 27 | 30 | 31 | 33 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |

## **Searching Program #2** - Ask the user to enter a target value and return the location of that value in the array. If the value does not exist, please inform the user.

#define NOTFOUNDERROR -1
#define ARRAYSIZE 15

int binarySearch(int[], int);
int getTarget(void);       //SAME FUNCTION USED IN SEQUENTIAL SEARCH PROGRAM

int main(void)
{
    int array[ARRAYSIZE] = {3, 5, 6, 10, 12, 15, 17, 18, 21, 22, 25, 27, 30, 31, 33};
    int target;            //VALUE WE ARE SEEKING
    int index;             //INDEX VALUE AT WHICH TARGET IS FOUND

    target = getTarget();
    index = binarySearch(array, target);

    if(index == NOTFOUNDERROR)
    {
        printf("Your value %d does not in the array!\n", target);
    }
    else
    {
        printf("Your value %d was found at index %d of the array.\n", target, index);
    }

    return(0);
}

int binarySearch(int x[], int n)
{
 int first = 0; //SMALLEST INDEX VALUE WE ARE CONSIDERING
 int last = ARRAYSIZE - 1; //LARGEST INDEX VALUE WE ARE CONSIDERING
 int mid; //MID POINT INDEX THAT WE ARE CONSIDERING
 int index = NOTFOUNDERROR; //VALUE TO RETURN WHICH INDICATES LOCATION OR NOT FOUND

do
{
 mid = (first + last) / 2;

 if(n > x[mid]) //TARGET GREATER THAN VALUE AT MID -> UPDATE FIRST
 {
 first = mid + 1;
 }
 else if(n < x[mid]) //TARGET LESS THAN VALUE AT MID -> UPDATE LAST
 {
 last = mid - 1;
 }
 else //TARGET HAS BEEN LOCATED IN THE ARRAY
 {
 index = mid;
 last = first - 1; //WHAT DOES THIS DO? WOULD first = last + 1 ALSO WORK?
 }
}while(first <= last);

 return(index);
}

The user-defined searching function will search the array until the `first` is greater than the `last` which would occur for one of the following reasons:

- The target is found.
- There are no elements in the array remaining as candidates to be searched.

## Multidimensional Arrays

The arrays we have seen so far are single dimension arrays. Each single dimension array is one row of indexed column values. Mastery of logic with single dimension arrays is necessary before considering multidimensional structures that may increase memory usage significantly.

With multidimensional arrays we can add a second dimension (multiple rows each with its own columns), a third dimension (planes, rows, and columns), and further as necessary. Your only limitation may be memory, but rarely does a problem call for an array with more than three dimensions.

Regardless of the number of dimensions in an array the name selected for the array will continue to represent the location where in memory its allocated space begins. We will see how this requires additional information to be communicated with functions that have a multidimensional array as a parameter.

## Declaration and Defining Multidimensional Arrays

Multidimensional arrays, like single dimension arrays, must be declared and defined before being used. Declaration and definition tell the compiler the name, data type, and size, or extent, of each dimension of the array.

| Data Type | Identifier | Dimension Extents |
|---|---|---|
| int | table | [4][4]; |

## Two-dimensional array:

- Each dimension is zero-based.
- The intersection of every row and column represents the capacity to store a value of the defined type.
- Total capacity is the product of the extent of each dimension.

## A three-dimensional array:

## A four-dimensional array:

Problem, calculate the average of each row in a two-dimensional array:

#define ROWS 5
#define COLS 4

void printTable(int[][COLS], float[]);
void calcAvgs(int[][COLS], float[]);

int main(void)
{
    float avgs[ROWS];
    int table[ROWS][COLS] =
    {
        {1, 2, 3, 4},
        {2, 3, 4, 5},
        {3, 4, 5, 6},
        {4, 5, 6, 7},
        {5, 6, 7, 8}
    };

    calcAvgs(table, avgs);
    printTable(table, avgs);

    return (0);
}
