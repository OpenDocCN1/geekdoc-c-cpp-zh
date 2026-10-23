```
found=true;
break;
}      // end of if
}      // end of for
return found;
}      // end of function
```

In the above example, element to be searched may be in the first position, in that case the complexity would be O (1). However in the majority of the cases it will be in the second position, third position or may be upto the nᵗʰ position. However, we consider its complexity as O (n).

# **C.   O(n²)**

Complexity of the type O (n²) is known as quadratic complexity. O (n²) results due to the nested loop involved in the algorithm. Consequently, for the 1ˢᵗ iteration of the external loop, the inner loop execute for ‘n’ times. Same has been depicted in the following example.

```
Problem: Write a program to sort the series of numbers using Bubble sort

Solution: Bubble sort method to sort the given array

void array (int arr [], int n)
{
int i, j;
for (i=0; i<n; i++)       // start of outer loop
{
    for (j=1; j<n-i; j++)   // inner loop
    {
        if (arr [j+1] > arr[j]) // comparing the elements
        {
                         // swapping if the adjacent is larger
temp=arr [j+1];
arr [j+1] =arr[j];
arr[j] =temp;
        }      // end of if
    }      //end of inner for loop
}      // end of outer for loop
}
```

Above example signifies that for the one iteration of outer loop, the inner loop executes ‘n-i’ times. Therefore, total number of iteration can be computed as:

n [n-1+n-2+n-3+………..3+2+1].