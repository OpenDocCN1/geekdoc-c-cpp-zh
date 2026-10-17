# 4.9. MULTIDIMENSIONAL ARRAYS

Till now the main area of concentration has been the one-dimensional arrays. Now you enter the area of ambiguity. This statement can be argued because the multidimensional arrays are defined in a pattern that resembles the one-dimensional array. The only disparity being that the multi dimensional array requires separate square brackets for each subscript. That is to say if the one dimensional array had a pair of square brackets, a two dimensional array will have two pairs of square brackets, three dimensional array three pairs of square brackets, and so on.

Two Dimensional Array A two dimensional array can be visualized as an array below an array. As earlier mentioned, a two dimensional array will have two pairs of square brackets. The description can be explained as below.

```
Data_type array_name [expression1] [expression2];
```

The two dimensional array is often referred to as a matrix. The expression one and two are the subscripts that the two-dimensional array will hold. Therefore, in the above expression one will specify the row and expression, two will specify the column and they indicate the number of array elements associated with each subscript.

Therefore if a declaration states:

```
int arr[4][2]
```

It means that a two dimensional array with the name arr is of integer type and has four rows and two columns. Its representation would be like this: Column No. 0 Column No. 1 Row no. 0 1000 10 Row no. 1 2000 20 Row no. 2 3000 30 Row no. 3 4000 40. Thus the element in arr[0][0] will be 1000 and the element in arr [3][2] will be 30. The rest of the numbers can be figured by having a look at the above table. In the memory the elements are placed in a sequential pattern such that the element in [0][0] will be first followed by the element in [0][1] followed by [1][0] and so on. Here too, each integer element will occupy two bytes.

Initializing a 2 dimensional Array Initializing a two dim array is as equivalent to initializing a one-dimensional array.

```
int sal[4][2]={{1000,10}, {2000,20}, {3000,30} {4000,40}}
```