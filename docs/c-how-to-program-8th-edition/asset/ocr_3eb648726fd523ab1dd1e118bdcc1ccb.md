next element. After the while loop ends, line 35 inserts the element into place. When the for statement in lines 21–36 terminates, the elements of the array are sorted.

The chief virtue of the insertion sort is that it’s easy to program; however, it runs slowly. This becomes apparent when sorting large arrays. In the exercises, we’ll investigate some alternate algorithms for sorting an array. We investigate sorting and searching in greater depth in Chapter 19.

# 7.9 Multidimensional Arrays

Arrays with two dimensions (i.e., subscripts) often represent tables of values consisting of information arranged in rows and columns. To identify a particular table element, we must specify two subscripts. By convention, the first identifies the element’s row and the second identifies the element’s column. Arrays that require two subscripts to identify a particular element are called two-dimensional arrays or 2-D arrays. Arrays with two or more dimensions are known as multidimensional arrays and can have more than two dimensions. Figure 7.20 illustrates a two-dimensional array. The array contains three rows and four columns, so it’s said to be a 3-by-4 array. In general, an array with m rows and n columns is called an m-by-n array.

![](bbox=[0.143, 0.464, 0.857, 0.667])

**Fig. 7.20** | Two-dimensional array with three rows and four columns.

Every element in an array a is identified in Fig. 7.20 by an element name of the form a[i][j], where a is the name of the array, and i and j are the subscripts that uniquely identify each element in a. Notice that the names of the elements in row 0 all have a first subscript of 0; the names of the elements in column 3 all have a second subscript of 3.

> **Common Programming Error 7.7**
> 
> Referencing a two-dimensional array element `a[x][y]` incorrectly as `a[x, y]` is an error. Actually, `a[x, y]` is treated as `a[x]`, because C++ evaluates the expression `x, y` (containing a comma operator) simply as `y` (the last of the comma-separated expressions).

A multidimensional array can be initialized in its declaration much like a one-dimensional array. For example, a two-dimensional array b with values 1 and 2 in its row 0 elements and values 3 and 4 in its row 1 elements could be declared and initialized with

```
int b[ 2 ][ 2 ] = { { 1, 2 }, { 3, 4 } };
```