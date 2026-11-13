# Example : WAP to input a 3 x 3 matrix and find out the sum of lower triangular elements.

```
#include<iostream.h>
void main()
{
int mat[3][3],i,j,sum=0;
```

![](bbox=[0.5, 0.15, 0.88, 0.28])

/* INPUT THE ARRAY */

```
for(i=0 ; i<3 ; i++)
for(j=0 ; j<3 ; j++)
{
cout<<"nEnter number";
cin>>mat[i][j];
}
```

/* LOGIC TO SUM THE LOWER TRIANGULAR ELEMENTS */

```
for(i=0 ; i<3 ; i++)
for(j=0 ; j<3 ; j++)
{
if(i>=j)
sum=sum+mat[i][j];
}
```

/* PRINT THE ARRAY */

```
cout<<"nTHE ENTERED MATRIX IS\n";
for(i=0 ; i<3 ; i++)
{
for(j=0 ; j<3 ; j++)
cout<<" "<<mat[i][j];
cout<<"\n";
}
cout<<"\nSum of the lower triangular matrix is"<<sum;
}
```