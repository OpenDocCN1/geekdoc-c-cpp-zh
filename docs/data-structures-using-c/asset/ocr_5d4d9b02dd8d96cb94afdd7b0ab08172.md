```
```cpp
{
if(val == A[low])
    return low;
else
    low++;
}
return -1;
}
```
```

```
```cpp
int main()
{
    int A[max] = {8,20,26,38,90,105,206,221,229,287,309,312,
    340,367,483,492,502,551,618,641,698,711,764,796};
    int index((max/8) + 1) = {0};
    int position;
    int key, i, choice;
    int opt = 0, pos = 0;
    cout << "Enter number to be searched : ";
    cin >> key;
    createIndex((index[0],(max/8) + 1,&A[0], max);
    pos = indexSeqSearch(key, index, (max/8) + 1, A, max);
    if(pos != -1)
    {
        cout << "found at position" << pos;
    }
    else
        cout << "not found";
    return 0;
}
```
```

```
```
/**********Output***************************************************************/
Enter number to be searched: 20
low = 0, high = 8
20 found at position 1

Enter number to be searched: 711
low = 16, high = 24
711 found at position 21

Enter number to be searched: 200
low = 0, high = 8
200 not found
***************************************************************/
```
```