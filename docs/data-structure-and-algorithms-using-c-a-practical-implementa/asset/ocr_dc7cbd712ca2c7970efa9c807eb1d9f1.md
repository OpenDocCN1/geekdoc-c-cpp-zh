```
quicksort(low, pi - 1);
      quicksort(pi + 1, high);
   }
   //merge sort
   void mergesort(int l, int r)
   {
   if (l < r)
   {
   int m = l+(r-l)/2;
   // Sort first and second halves
   mergesort(l, m);
   mergesort(m+1, r);
   merge(l, m, r);
   }
   }
```

```
void merge(int l, int m, int r)
{
int i, j, k;
int n1 = m - l + 1;
int n2 = r - m;
int L[n1], R[n2];
for (i = 0; i < n1; i++)
L[i] = a[l + 1];
for (j = 0; j < n2; j++)
R[j] = a[m + 1 + j];
i = 0;
j = 0;
k = l; //index for merge array
while (i < n1 && j < n2)
{
if (L[i] <= R[j])
{
a[k] = L[i];
i++;
}
else
{
a[k] = R[j];
j++;
}
}
```