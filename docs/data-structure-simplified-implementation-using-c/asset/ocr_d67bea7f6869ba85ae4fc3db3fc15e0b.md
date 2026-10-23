```
if (min > a[j])
{
min=a[j];
index=j;
cout<<" Min "<<min<<"index="<<j<<endl;
}
}
if (i! =j)//item is not the minimum
{
a [index] =a[i];
a[i] =min;
}
```

# 10.4 EFFICIENT SORTING ALGORITHMS

All the algorithms that are discussed above worked on the principle of exchange, as a result, the algorithm were less efficient. All of them were having the complexity of O (n²). Their efficiency having compared hereunder:

Table 10.1: Values for various N

|  | N= | 1 | 100 | 1000 |
| efficiency |  |  |  | |
| N | 1 | 100 | 1000 |
| N² | 1 | 10000 | 1000000 |
| logN | 0 | 4.60 | 6.9 |

Therefore, we need algorithm that should result in better performance. Algorithm discussed below gives better performance.

# A. Bucket sort

In the bucket sort algorithm, we arrange the items in groups based on their category. These categories of items are decided by the start value. For instance, consider the series 28, 17, 40, 99, 27, 22, 96, 98. In this series, items are arranged as per their weight in a group. Series with 1 in tenth places is grouped in one bucket, similarly numbers at tenth position is 2, and it will be grouped into 2nd group. Process will continue upto the value of 9. For the given series, bucket has been illustrated in the following figure.