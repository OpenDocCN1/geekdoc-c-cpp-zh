# 9.3 Organizing Data in Linear Collections — 391

Initial state:

[5 4 10 20 12 3]

1. Pick 3

[5 4 10 20 12 3]

2. Pick 4

3 [4 10 20 12 5]

3. Pick 5

3 4 [10 20 12 5]

4. Pick 10

3 4 5 [20 12 10]

5. Pick 12

3 4 5 10 [12 20]

After sort:

3 4 5 10 12 [20]

Fig. 9.20: Procedure of direct selection sort.

```
//Tool function: swap the value of x and y
template <class T>
void Swap (T &x, T &y)
{
  T temp;
  temp = x;
  x = y;
  y = temp;
}
```

```
//Use selection sort to sort the n elements in array A
template <class T>
void SelectionSort(T A[], int n)
{
  int startIndex;             //Select the index of minimum
  int i, j;                   //element every turn
  for (i = 0; i < n-1; i++)
{
    startIndex = i;         //The initial index of minimum
}
```