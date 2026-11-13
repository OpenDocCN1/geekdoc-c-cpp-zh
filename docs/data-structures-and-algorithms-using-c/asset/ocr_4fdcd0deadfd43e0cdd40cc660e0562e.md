```
printf("Updated Array : ");
display();
return leftPointer;
}
void quickSort(int left, int right){
if(right-left <= 0){
return;
}
}else {
int pivot = intArray[right];
int partitionPoint = partition(left, right, pivot); quickSort(left,partitionPoint-1);
quickSort(partitionPoint+1,right);
}
}
main(){
printf("Input Array : "); display();
printline(50);
quickSort(0,MAX-1);
printf("Output Array : "); display();
printline(50);
}
```

If we compile and run the above program, it will produce the following result – Input Array: [4 6 3 2 1 9 7]

```
pivot swapped :9,7
Updated Array: [4 6 3 2 1 7 9 ]
pivot swapped :4,1
Updated Array: [1 6 3 2 4 7 9 ]
item swapped :6,2
pivot swapped :6,4
Updated Array: [1 2 3 4 6 7 9 ]
pivot swapped :3,3
Updated Array: [1 2 3 4 6 7 9 ]
Output Array: [1 2 3 4 6 7 9 ]
```