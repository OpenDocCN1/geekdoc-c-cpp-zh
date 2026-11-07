+   b. First row of beta: 0 1 2
+      Second row of beta: 1 2 3
+      Third row of beta: 2 3 4

+   c. First row of beta: 0 0 0
+      Second row of beta: 0 1 2
+      Third row of beta: 0 2 4

+   d. First row of beta: 0 2 0
+      Second row of beta: 2 0 2
+      Third row of beta: 0 2 0

# Chapter 10

+   1. a. false; b. true; c. false; d. false; e. false

```
3. a.
```cpp
int seqOrderedSearch(const int list[], int listLength,
                     int searchItem)
{
    int loc;
    bool found = false;

    for (loc = 0; loc < listLength; loc++)
        if (list[loc] >= searchItem)
        {
            found = true;
            break;
        }

    if (found)
        if (list[loc] == searchItem)
            return loc;
        else
            return -1;
    else
        return -1;
}
```
```

+   b. i. 5   ii. 7   iii. 8   iv. 11

+   5. List before the first iteration: 26, 45, 17, 65, 33, 55, 12, 18
+      List after the first iteration: 26, 17, 45, 33, 55, 12, 18, 65
+      List after the second iteration: 17, 26, 33, 45, 12, 18, 55, 65
+      List after the third iteration: 17, 26, 33, 12, 18, 45, 55, 65
+      List after the fourth iteration: 17, 26, 12, 18, 33, 45, 55, 65
+      List after the fifth iteration: 17, 12, 18, 26, 33, 45, 55, 65
+      List after the sixth iteration: 12, 17, 18, 26, 33, 45, 55, 65
+      List after the seventh iteration: 12, 17, 18, 26, 33, 45, 55, 65

+   7. 3