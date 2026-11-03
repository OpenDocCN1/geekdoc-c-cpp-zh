```
while(dir>=esq) {i=(esq+dir)/2;
    if (element==mat[i]) return i;
    if (element < mat[i]) dir=i-1;
    else esq=i+1;}  return -1;
}
void Quicksort(int a[], int h, int r)
/* Quicksort Algorithm */
{ int i,j,x,t; i=h;j=r;x=a[(h+r)/2];
do
{ while(a[i]<x)i++; while(x<a[j])j--;
    if(i<=j) {t=a[i];a[i]=a[j];a[j]=t;i++;j--};}
} while(i<=j);
if(h<j) Quicksort(a,h,j);
if(i<r) Quicksort(a,i,r);
}
int main()                /* Searching */
{ int i, element=0; srand(time(NULL)); /*Creating array*/
for(i=0;i<TOTAL;i++) mat[i]=rand();
puts("\n Matriz ordenada: ");  /* Sorting array */
Quicksort(mat, 0, TOTAL-1);
for(i=0;i<TOTAL;i++) printf("%8d",mat[i]);
while(element!=-1)
{ puts("\n (Type -1 to exit "); /* Searching element */
    printf("\n What value do you want find? ");
    scanf("%d",&element); fflush(stdin);
    if(element>=0) {i=Binarysearch(element);
        if (i>=0)
printf("Pronto! mat[%d]=%d",i,mat[i]);
    else
printf("\nArray doesn’t contain the element %d",
element);}
```