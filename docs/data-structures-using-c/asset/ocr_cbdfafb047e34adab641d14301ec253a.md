Let these elements be placed in an array named Numbers. Now, we can have another array of 10 elements that will show the Frequency of each value in the list Numbers.

```
void FrequencyCount(int Freq[10], int A[100])
{
   int i;
   for(i = 0; i < 10; i++)
      Freq[i] = 0;
   for(i = 0; i < 100; i++)
      Freq[A[i]]++;
}
```

In Fig. 2.26, Frequency[0] indicates that 0 occurred once in the array Numbers, 1 appeared 20 times, 2 appeared 5 times, and so on.

![](bbox=[0.22, 0.35, 0.88, 0.51])

Fig. 2.26 Frequency count of numbers ranging from 0 to 9

This concept will be used in Section 2.11.3 for fast transpose.

# 2.11 SPARSE MATRIX

A matrix is a very commonly used mathematical object. To represent a matrix, we need a two-dimensional array with two different indices for row and column references. The representation of a matrix for operations on it should be efficient so that the space and time requirement is less.

In many applications, the crucial aspect for algorithm design is space consideration. So the developer has to take care of the representation of the matrix if it is large. In many situations, the matrix size is very large but most of the elements in it are 0s (less important or irrelevant data). Only a small fraction of the matrix is actually used. A matrix of such type is called a sparse matrix, as the matrix is filled sparsely by data and most of the positions are empty or contain non-relevant data. In such cases, the matrix must be represented and stored with an alternate representation to achieve good space utilization. Such representation avoids operations such as operations with 0s (addition or multiplication of 0s). Consequently, a good time complexity along with efficient storage is achieved if a sparse matrix is stored with an alternate representation rather than the conventional way.