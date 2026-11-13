```
}
int partition(int A[],int low, int high)
{
 int pivot, i, j;
 pivot = A[low];
 j = high + 1; i = low;
 do
 {
 i++;
 while(A[i] < pivot && low <= high)
 do
 j--;
 }while(pivot < A[j]);
 if(i < j)
 swap(A[i],A[j]);
 }while(i < j);
 A[low] = A[j];
 A[j] = pivot;
 return j;
}
```

```
main()
{
 int A[max], n;
 int i, choice;
 cout << "Enter number of numbers: ";
 cin >> n;
 cout << "Enter numbers: ";
 read(A, n);
 qsort(A, 0, n - 1);
 cout << "Sorted array is: ";
 display(A, n);
}
```

```
/********************************Output********************************
Enter number of numbers: 7
Enter numbers: 10 5 23 67 20 30 60
Sorted array is: 5 10 20 23 30 60 67
**************************************************************/
```