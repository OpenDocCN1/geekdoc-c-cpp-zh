Ans:

```
```cpp
int sum ( int n)
{

    if(n==1) return 1;
    else return n+sum (n-1);
}
```
```

# Q13: What is the need of array? Write a C++ program to find the sum of column element of a two dimensional N X N array A (Mumbai University, May 2009)

Ans:

```
```cpp
#include<iostream.h>

void main()
{
    int A[10][10];

    int N;
    cin>>N;

    for (int K=1; K<=N;K++)
    for (int I=1;I<=N; I++)
    cin>>A[K][I];

    int Sum=0;
    for (K=1; K<=N;K++)
    for (I=1;I<=N; I++)
    Sum=Sum +A[I][K];

    cout<<"\n Sum of Elements"<<Sum;
}
```
```

# Q14: Write a program to demonstrate call by reference (Mumbai University, December 2008)

Ans:

```
```cpp
#include<iostream.h>
#include<conio.h>

void swap(int &A, int &B)
{
    int temp=A;
```
```