```
printf("a = %d, b = %d\n", a, b);
swap(&a, &b);
printf("a = %d, b = %d\n", a, b);
system("pause");
}
```

# 5.7.5 BubbleSort

```
void bubble(int a[], int n)
{
int i, j;
for (i 0; i < n; ++i)
for (j n 1; j > i; -j)
if (a[j 1J > a[j])
swap(&a[j-1], &a[jJ);
}
```

![](bbox=[0.18, 0.7, 0.7, 0.8])

# Chapter 6: Arrays, Pointers and
Strings

C provides a data structure that can store multiple values of same type in it by