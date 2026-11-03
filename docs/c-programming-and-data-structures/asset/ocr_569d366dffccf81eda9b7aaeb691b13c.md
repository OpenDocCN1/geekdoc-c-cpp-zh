```
{
case 1:
printf("Input rows and columns of A & B Matrix:");
scanf("%d%d",&r1,&c1);
printf("Enter elements of matrix A:\n");
for(i=0;i<r1;i++)
{
for(j=0;j<c1;j++)
scanf("%d",&a[i][j]);
}
printf("Enter elements of matrix B:\n");
for(i=0;i<r1;i++)
{
for(j=0;j<c1;j++)
scanf("%d",&b[i][j]);
}
printf("\n =====Matrix Addition=====\n");
for(i=0;i<r1;i++)
{
for(j=0;j<c1;j++)
printf("%5d",a[i][j]+b[i][j]);
printf("\n");
}
break;

case 2:
printf("Input rows and columns of A matrix:");
scanf("%d%d",&m,&n);
printf("Input rows and columns of B matrix:");
scanf("%d%d",&p,&q);
if(n==p)
{
printf("matrices can be multiplied\n");
printf("resultant matrix is %d*%d\n",m,q);
printf("Input A matrix\n");
read_matrix(a,m,n);
printf("Input B matrix\n");
/*Function call to read the matrix*/
read_matrix(b,p,q);
/*Function for Multiplication of two matrices*/
printf("\n =====Matrix Multiplication=====\n");
for(i=0;i<m;i++)
for(j=0;j<q;j++)
{
c[i][j]=0;
for(k=0;k<n;k++)
c[i][j]=c[i][j]+a[i][k]*b[k][j];
}
printf("Resultant of two matrices:\n");
write_matrix(c,m,q);
}
/*end if*/
else
{
printf("Matrices cannot be multiplied.");
}
}
```