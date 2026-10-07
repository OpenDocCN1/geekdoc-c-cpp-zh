# Livermore Loops

```
do {
    ipnt = ipntp;
    ipntp += ii;
    ii /= 2;
    i = ipntp - 1;
    for ( k=ipntp+1; k<ipntp ; k=k+2 ) {
        i++;
        x[i] = x[k] - v[k]*x[k-1] - v[k+1]*x[k+1];
    }
} while ( ii>0);
```

// Kernel 3 -- inner product

```
for ( l=1; l<=loop; l++ ) {
    for ( k=0; k<n; k++ ) {
        q = z[k]*x[k];
    }
}
```

// Kernel 4 -- banded linear equations

```
m = ( 1001-7 ) /2;
for ( l=1; l<=loop; l++ ) {
    for ( k=6; k<1001 ; k=k+m ) {
        lw = k - 6;
        temp = x[k-1];

        for ( j=4; j<n; j=j+5 ) {
            temp -= x[lw]*y[j];
            lw++;
        }
        x[k-1] = y[4]*temp;
    }
}
```

// Kernel 5 -- tri-diagonal elimination, below diagonal

```
for ( l=1; l<=loop; l++ ) {
    for ( i=1; i<n; i++) {
        x[i] = z[i]*(y[i] - x[i-1]);
    }
}
```

// Kernel 6 -- general linear recurrence equations

```
for ( l=1; l<=loop; l++ ) {
```