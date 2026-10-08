
```
if array[i] = item-to-find
  set location to i
else
  i <- i + 1
end if
end while
return the location
end
```

In the worst possible case, a linear search of an array containing n elements requires n comparisons. The best case requires one comparison. On the average, (n + 1)/2 comparisons are required to access any element with equal probability of accessing every element. The linear search is said to be of order of n.

# Program

```
********************************************************************************/
/* main: Linear Search */
********************************************************************************/
/* Defined Constants: */
/*  ARSIZE - array size searched */
/*  Input Variables: */
/*  array[ARSIZE] - the array of values to be */
/*  searched */
/*  value - value to be found */
/*  Output Variables: */
/*  value - value to be found */
/*  location - location of the value to be found */
/*  array[location] - value found */
/* Functions Called: */
/*  funcsearch() - linear search */
/********************************************************************************/
```

## 450 One-Dimensional Arrays

```
#include <stdio.h>

#define ARSIZE 5

int funcsearch(float [ ], float, int n);
int main() {
    float array[ARSIZE], value;
    int flag, location, i;

    printf("Enter the values for the array: \n");
    for(i = 0; i < ARSIZE; i++)
        scanf("%f", &array[i]);

    printf("Enter the value to be found: \n");
    scanf("%f", &value);

    location = funcsearch(array, value, ARSIZE);

    if(location >= 0)
        printf("\n%4.1f is found in position %d", array[location], location + 1);
    else
        printf("\n%4.1f is not found\n", value);

    return 0;
}
```

```
****************************************************
/* funcsearch: Linear Search */
****************************************************

****************************************************
/* Input Parameters: */
/* array[n] - the array of values to be */
/*           searched */
/* value - value to be found */
/* n - size of array */
****************************************************
********************************************************************
/* Output Parameters: */
/* location - position of the value found */
****************************************************
/* Return variables: */
/* flag - success flag */
****************************************************
```

```
int funcsearch(float array1[ ], float value1, int n)
{
    int i, location = -1;
    for(i = 0; i < n; i++)
    {
        if(array1[i] == value1)
        {
            location = i;
            i = n;
        }
    }
    return location;
}
```

# Input and Output

===========
Enter the values for the array:
23.5 65.7 78.4 15.6 47.8

Enter the value to be found:
15.6

15.6 is found in position 4

Enter the values for the array:
23.5 65.7 78.4 15.6 47.8

Enter the value to be found:
56.7

56.7 is not found

**Binary Search** On the average, the linear search requires half of the list to locate an item in the list. This is very inefficient for sorted lists. A binary search is more efficient for sorted lists than a linear search. A binary search uses a probing procedure to look at the middle element of the list and determines which half the desired element is in. Then it looks at the middle element of that half to determine which quarter of the list contains the desired element. By repeatedly halving the search list, the element can be located very quickly.

## Binary Search

Suppose we want the number 5 in the following list:

| SORTED LIST | PROBE 1 | PROBE 2 | PROBE 3 | PROBE 4 |
| :--- | :--- | :--- | :--- | :--- |
| | | | | |
| | | | | |
| | | | | |
| | | | | |
| | | | | |

## Pseudocode

```
main:
  input the sorted array
  call funcsearch()
  if found
    output location
  else
    output message
  stop

funcsearch:
  position <- -1
  first <- 0
  last <- n - 1
  while first <= last
    middle <- (first + last) / 2
    if(array[middle] > value)
      last <- middle - 1
    else if(array[middle] < value)
      first <- middle + 1
    else
      position = middle
end while
return position
```
