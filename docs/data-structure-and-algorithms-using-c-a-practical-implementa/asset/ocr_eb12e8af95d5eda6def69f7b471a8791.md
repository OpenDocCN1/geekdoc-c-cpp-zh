```
```c
for(k = 2 ; k < n; ++k)
{
    i = k ;
    temp = list[k] ;
    j = i / 2 ;
    while((i > 1) && (temp > list[j]))
    {
        list[i] = list[j] ;
        i = j ;
        j = i / 2 ,
        if ( j < 1 )
            j = 1 ;
    }
    list[i] = temp ;
}
}
```
```

```
```c
void heap(int arr[], int n)
{
    int k, temp, value, j, i, p;
    int step = 1;
    for(k = n ; k >= 2; --k)
    {
        temp = arr[1] ;
        arr[1] = arr[k] ;
        arr[k] = temp ;

        i = 1 ;
        value = arr[1];
        j = 2 ;

        if((j+1 < k)
        {
            if(arr[j+1] > arr[j])
                j ++;
        }
        while((j << k) && (arr[j] > value))
        {
            arr[i] = arr[j];
            i = j ;
            j = 2*i ;
            if((j+1) < k)
            {
                if(arr[j+1] > arr[j])
                    j++;
            }
            else
                if ( j > n)
                    j = n ;
        }
    }
}
```
```