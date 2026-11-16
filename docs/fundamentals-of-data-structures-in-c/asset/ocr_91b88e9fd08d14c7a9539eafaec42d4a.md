```
```c
printf("The greatest common divisor is %ld", gcd(a, n, 2 ));
}
```
```

```
```c
int check_limit(int a[], int n, int prime)
{
    int i;

    for(i = 0; i < n; i++)
        if(prime > a[i])
            return 1;
    return 0;
}
```
```

```
```c
int check_all(int a[], int n, int prime)
{
    int i;

    for(i = 0; i < n; i++)
        if((a[i] % prime) != 0)
            return 0;

    for(i = 0; i < n; i++)
        a[i] = a[i] / prime;
    return 1;
}
```
```

```
```c
long int gcd(int a[], int n, int prime)
{
    int i;

    if(check_limit(a, n, prime))
        return 1;

    if(check_all(a, n, prime))
        return(prime * gcd(a, n, prime));
    else
        return(gcd(a, n, prime = (prime == 2) ? prime+1 : prime+2));
}
```
```

```
```
The program displays the following output
Enter the limit : 5
Enter the numbers : 99 55 22 77 121
The greatest common divisor is 11
```
```