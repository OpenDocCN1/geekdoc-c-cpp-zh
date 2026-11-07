+   27. Answer to this question is available at the Web site accompanying this book.
+   29. Answer to this question is available at the Web site accompanying this book.

# Chapter 19

+   1. a. false; b. true; c. false; d. false
+   3. a.

```
template <class elemType>
int seqOrdSearch(const elemType list[], int length,
                 const elemType& item)
{
    int loc;
    bool found = false;

    for (loc = 0; loc < length; loc++)
        if (list[loc] >= item)
        {
            found = true;
            break;
        }

    if (found)
        if (list[loc] == item)
            return loc;
        else
            return -1;
    else
        return -1;
} //end seqOrdSearch
```

+   b. i. 5  ii. 7  iii. 8  iv. 11
+   5. 26
+   7. a.

Suppose that the list is of length n. Then length = n. Consider the first iteration of the outer for loop, that is, when the value of iteration = 1. Now the inner loop executes n − 1. Before the execution of the inner for loop, the variable isSorted is set to true, assuming that the list is sorted. If the list is already sorted, then the expression list[index] > list[index + 1] in the if statement always evaluates to false, so the body of the if statement never executes. Because the inner loop executes n − 1 times, there are n − 1 comparisons. In the second iteration of the outer loop, because the variable isSorted is true, the loop condition (iteration < length) && !isSorted evaluates to false, so the outer for loop terminates. It follows that, if the list is already sorted, the outer for loop executes only once. Hence, the total number of comparisons is n − 1 = O(n).

+   b. 30