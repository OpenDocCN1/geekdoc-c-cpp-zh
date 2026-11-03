
```c
printf("\nThe key is not found in the list");
}
void bubblesort(int elements[], int maxsize)
{
    int i, j, temp;
    for (i = 0; i < maxsize - 1; i++)
    {
        for (j = i; j < maxsize; j++)
        {
            if (elements[i] > elements[j])
            {
                temp = elements[i];
                elements[i] = elements[j];
                elements[j] = temp;
            }
        }
    }
}
int binsearch(int elements[], int maxsize, int key)
{
    int i, first, middle, last;
    first = 0;
    last = maxsize - 1;
    while (last >= first)
    {
        middle = (first + last) / 2;
        if (key > elements[middle])
            first = middle + 1;
        else if (key < elements[middle])
            last = middle - 1;
        else
            return middle;
    }
    return -1;
}
```

## Fig. 17.9

In the above program, a bubble sort function is also added to get a sorted list before applying binary search on the list. Instead of the bubble sort, you can adopt any other sort routine, which we have already discussed in previous sections.

In the program, you can infer that we have used the variable ‘middle’ to locate our key. All the comparisons are based on the element, which is at the position pointed by the variable ‘middle’. This variable is altered continuously till we get the result. If the search fails, the function returns a negative value.

## 2. C program for Recursive binary search

We can write a recursive version of the binary search also very easily. Figure 17.10 gives program for such a version of binary search.

```
#include <stdlib.h>
#include <stdio.h>

#define MAXSIZE 500

int binsearch(int elements[], int maxsize, int key, int first, int last);
void bubblesort(int elements[], int maxsize);
int elements[MAXSIZE], maxsize, key;
int main()
{
    int i, pos;
    printf("\nHow many elements you have in the list: ");
    scanf("%d",&maxsize);
    printf("\nEnter the key to be searched: ");
    scanf("%d",&key);
    printf("\nEnter the values one by one: ");
    for (i = 0; i < maxsize; i++)
    {
        printf ("\nEnter element %i : ");
        scanf("%d",&elements[i]);
    }
    bubblesort(elements, maxsize);
    pos = -1;
    pos = binsearch(elements, maxsize, key, 0, maxsize - 1);
    if (pos != -1)
        printf("\nThe key %d is found at position %d", key, pos);
    else
        printf("\nThe key is not found in the list");
}
void bubblesort(int elements[], int maxsize)
{
    int i, j, temp;
    for (i = 0; i < maxsize - 1; i++)
    {
        for (j = i; j < maxsize; j++)
        {
            if (elements[i] > elements[j])
            {
                temp = elements[i];
                elements[i] = elements[j];
                elements[j] = temp;
            }
        }
    }
```

```
}
}
int binsearch(int elements[], int maxsize, int key, int first, int last)
{
int i, middle;
middle = -1;
if (first <= last)
{
middle = (first + last) / 2;
if (key > elements[middle])
middle = binsearch(elements, maxsize, key, middle + 1, last);
else if (key < elements[middle])
middle = binsearch(elements, maxsize, key, first, middle - 1);
}
return middle;
}
```

### Fig. 17.10

## 17.3.3 Indexed Sequential search

Yet another searching technique is the indexed sequential search. This is widely employed in various file handling and database systems. The method is based on a "short representation" of the list. This "short representation" is called as index. How this index is formed? Many ways do exist to form this index. One of the widely used ways is to extract every eighth element from the list and make that as a part of the index.

Whenever a particular key is to be searched, it is first searched in the index. The appropriate location from the index is taken and that location is sequentially searched. Figure 17.11 explains this scenario. In the figure, every fifth record is taken as an example.

![](img/65953ea584e494f3d396b2252cb5ea53_489_0.png)

### Fig. 17.11

In Fig. 17.11, assume that we are searching for 16. The index is first searched. Note that you may not get an exact match for the key in the index. You will get only the range, which you may use for searching the main list. In this example, we get the range that 16 is between 14 and 29. You may perform a sequential search in this range to get at the key value.

## POINTS TO REMEMBER

- 1. Sorting means rearranging a given list in an orderly manner. Searching is the process of locating a particular key from a list.
- 2. The efficiency of a sorting algorithm is expressed in terms of the O-notation.
- 3. A sorting algorithm with O(log n) is supposed to be a highly efficient sorting algorithm.
- 4. The efficiency of bubble sort, insertion sort, selection sort and shell sort is O(n). The efficiency of heap sort, merge sort and quick sort is O(n log n).
- 5. Quick sort designed by Hoare is a very efficient sorting algorithm.
- 6. Binary search may be combined with the indexed sequential searching to give better efficiency.
- 7. Always remember that searching in a sorted list is more efficient than searching in an unsorted list.

## Review Questions

- 17.1 Discuss bubble sort, write a C program and show its efficiency.
- 17.2 Discuss the quick sort. Derive the efficiency of the quick sort in the best and worst cases.
- 17.3 What is a heap? Show how would you perform a heap sort using a heap? Work out the efficiency factor of the heap sort.
- 17.4 Show that the efficiency of quick sort in its worst case is the same as that of simple insertion sort.
- 17.5 Show that shell sort is based on the insertion sort.
- 17.6 Discuss the linear search method.
- 17.7 Explain the binary searching with a C program.
- 17.8 What is an index? How can an index speed up the search process?

## State whether the following statements are True or False

- (a) Sorting and searching are always tightly interrelated.
- (b) Quick sort's efficiency relies on the pivot.
- (c) Bubble sort even though simple is very efficient.
- (d) Selection sort is based on binary tree.
- (e) Shell sort is based on quick sort.
- (f) Quick sort uses a divide-and-conquer approach.
- (g) A sorting method whose efficiency is O(2^n) means that the amount of time the algorithm will take to complete doubles each time you increase the input.
- (h) A sorting method with O(log n) is the most efficient method.
- (i) Sorting is mandatory for linear searching.
- (j) Binary search can be done on an ordered list only.
- (k) Indexed sequential search can be applied to file handling only and not to list.
- (l) The choice of constructing the index by picking every third number from the main list can be changed.

## Answers to True and False Questions

- (a) False    (b) True    (c) False    (d) False    (e) False
- (f) True    (g) True    (h) True    (i) False    (j) True
- (k) False    (l) True

## Appendix A

## ASCII Values of Characters

| ASCII Value | Character | ASCII Value | Character | ASCII Value | Character | ASCII Value | Character |
|---|---|---|---|---|---|---|---|
| 000 | NUL | 032 | blank | 064 | @ | 096 | ` |
| 001 | SOH | 033 | ! | 065 | A | 097 | a |
| 002 | STX | 034 | " | 066 | B | 098 | b |
| 003 | ETX | 035 | # | 067 | C | 099 | c |
| 004 | EOT | 036 | $ | 068 | D | 100 | d |
| 005 | ENQ | 037 | % | 069 | E | 101 | e |
| 006 | ACK | 038 | & | 070 | F | 102 | f |
| 007 | BEL | 039 | ' | 071 | G | 103 | g |
| 008 | BS | 040 | ( | 072 | H | 104 | h |
| 009 | HT | 041 | ) | 073 | I | 105 | i |
| 010 | LF | 042 | * | 074 | J | 106 | j |
| 011 | VT | 043 | + | 075 | K | 107 | k |
| 012 | FF | 044 | , | 076 | L | 108 | l |
| 013 | CR | 045 | - | 077 | M | 109 | m |
| 014 | SO | 046 | . | 078 | N | 110 | n |
| 015 | SI | 047 | / | 079 | O | 111 | o |
| 016 | DLE | 048 | 0 | 080 | P | 112 | p |
| 017 | DC1 | 049 | 1 | 081 | Q | 113 | q |
| 018 | DC2 | 050 | 2 | 082 | R | 114 | r |
| 019 | DC3 | 051 | 3 | 083 | S | 115 | s |
| 020 | DC4 | 052 | 4 | 084 | T | 116 | t |
| 021 | NAK | 053 | 5 | 085 | U | 117 | u |
| 022 | SYN | 054 | 6 | 086 | V | 118 | v |
| 023 | ETB | 055 | 7 | 087 | W | 119 | w |
| 024 | CAN | 056 | 8 | 088 | X | 120 | x |
| 025 | EM | 057 | 9 | 089 | Y | 121 | y |
| 026 | SUB | 058 | : | 090 | Z | 122 | z |
| 027 | ESC | 059 | ; | 091 | [ | 123 | { |
| 028 | FS | 060 | < | 092 | \ | 124 | \| |
| 029 | GS | 061 | = | 093 | ] | 125 | } |
| 030 | RS | 062 | > | 094 | ^ | 126 | ~ |
| 031 | US | 063 | ? | 095 | _ | 127 | DEL |

Note: The first 32 characters and the last character are control characters; they cannot be printed.
