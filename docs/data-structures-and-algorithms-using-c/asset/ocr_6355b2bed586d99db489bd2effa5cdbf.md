# QuickSortPseudocode

To get more into it, let see the pseudocode for quick sort algorithm – procedure quickSort(left, right)

```
if right-left <= 0
return
else
pivot = A[right]
partition = partitionFunc(left, right, pivot) quickSort(left,partition-1)
quickSort(partition+1,right)
end if
```

end procedure To know about quick sort implementation in C programming language, please click here.