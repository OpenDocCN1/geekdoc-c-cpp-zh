```
```cpp
if (j==1) {
    T coef = 1. / power(2,i+k);
    if(item[48])
        item[48]->append(coef,J);
    else
        item[48] = new row<T>(coef,J);
}
if(!j&&!(i||k)){
    T coef = (i+k) / sqrt(2.) / power(2,i+k-1);
    if(item[49])
        item[49]->append(coef,J);
    else
        item[49] = new row<T>(coef,J);
}
```
```

Similarly, the next two rows correspond to the edge midpoint (0,1/2,1/2). The normal derivatives at this point are the x-partial derivative and the sum of the y- and z-partial derivatives, divided by √2:

```
```cpp
if (k==1) {
    T coef = 1. / power(2,i+j);
    if(item[50])
        item[50]->append(coef,J);
    else
        item[50] = new row<T>(coef,J);
}
if(!k&&!(i||j)){
    T coef = (i+j) / sqrt(2.) / power(2,i+j-1);
    if(item[51])
        item[51]->append(coef,J);
    else
        item[51] = new row<T>(coef,J);
}
```
```

The final four rows correspond to side midpoints of T. In particular, the next row corresponds to the normal derivative (or the z-partial derivative) at (1/3,1/3,0):

```
```cpp
if (i==1) {
    T coef = 1. / power(3,j+k);
    if(item[52])
        item[52]->append(coef,J);
    else
        item[52] = new row<T>(coef,J);
}
```
```

Furthermore, the next row corresponds to the normal derivative (or the y-partial derivative) at (1/3,0,1/3):