# Performance Measuring

# Algorithm 11 C Program - Exercise 23

```
#include <systime.h>
#include <stdio.h>
#include <stdlib.h>
int *mrat(int al2, int mn) {
    struct timeval tv;
    gettimeofday(&tv,NULL);
    int *as = 0;
    int i;
    as = (int*)malloc(al2*sizeof(int));
    rand() % tv.tvusec;
    for(i=0; i<al2; ++i)
    as[i] = (random() % (mn - 2)) + 2;
    return as;
}
int ip(int x) {
    int y;
    for(y=2; y< x; ++y)
    if(x % y) == 0
        return 1;
    return 0;
}
int *fp(int al3, int arr[]) {
    int *as = 0;
    int i;
    as = (int*)malloc(al3*sizeof(int));
    for(i=0; i<al3; ++i)
    if(ip(arr[i]))
        as[i] = 1;
    return as;
}
int fl(int al4, int *nums, int *ips) {
    if(al4<=0)
        return -1;
    if(ips[al4-1])
        return fl(al4-1,nums,ips);
    return nums[al4-1];
}
void vp(int al5, int *nums, int *ips, int l1) {
    int i;
    for(i=0; i<al5; ++i)
    if(ips(nums[i]])
        printf("%d\tThe largest prime is %d\n\", nums[i], l1);
}
int main() {
    int i, l1, al1, mn1;
    int *ra = 0;
    int *pr = 0;
    int k = 1000;
    al1 = 25;
    al2 = 10000;
    mn1 = 1000;
    printf("Generate %d list(s) of size %d of primes - Each prime is 0, %d)\t\n\n\", mn1, al1, k, mn1, 0);
    for(i=0; i<k; ++i) {
        al = al1;
        mn = mn1;
        ra = mrat(al,mn);
        pr = fp(al,ra);
        l = fl(al,pr);
        printf("List number %d\t%i\n", l, i);
        free(ra);
        free(pr);
    }
    return 0;
}
```