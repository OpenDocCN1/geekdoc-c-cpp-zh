Lab Programming

1 2 3 4
1 2 3 4 5

# 25. Write a C program to reverse a sentence using recursion.

```
#include<stdio.h>
voidreverseSentence();
    int main(){
    printf("Enter a sentence: ");
```

Output
nEnter a sentence: IndrakantiSekhar
SekharIndrakanti

# 26. Write a C Program to display prime numbers between intervals using function.

```
#include<stdio.h>
intcheckPrimeNumber(int n);
int main(){
    int n1, n2, i, flag;
    printf("Enter two integers: ");
    scanf("%d %d",&n1,&n2);
    printf("Prime numbers between %d and %d are: ", n1, n2);
    for(i=n1+1; i < n2;i++){

    // flag will be equal to 1 if i is prime
    flag=checkPrimeNumber(i);

    if(flag==1)
    printf("%d ", i);
    }
    return0;
}
```