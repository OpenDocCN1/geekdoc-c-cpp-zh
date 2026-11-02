# 6.1.2 Accessing Array Elements

Individual elements in an array values are accessed by an integer index i, using the notation values[i].

The values stored in an array are called its elements. Each element has a position number, called an index. To access a value in the values array, you must specify which index you want to use. That is done with the [] operator:

```
values[4] = 34.5;
```

Now the element with index 4 is filled with 34.5. (See Figure 2).

![](bbox=[0.42, 0.36, 0.78, 0.6])

Figure 2 Filling an Array Element

You can display the contents of the element with index 4 with the following command:

```
cout << values[4] << endl;
```

As you can see, the element values[4] can be used like any variable of type double.

An array element can be used like any variable.

In C++, array positions are counted in a way that you may find surprising. If you look carefully at Figure 2, you will find that the fifth element was filled when we changed values[4]. In C++, the elements of arrays are numbered starting at 0. That is,

+   - values[0], the first element
+   - values[1], the second element
+   - values[2], the third element
+   - values[3], the fourth element
+   - values[4], the fifth element
+   - ...
+   - values[9], the tenth element

You will see in Chapter 7 why this numbering scheme was chosen in C++.

You have to be careful about index values. Trying to access a element that does not exist in the array is a serious error. For example, if values has twenty elements, you are not allowed to access values[20].

An array index must be at least zero and less than the size of the array.

![](bbox=[0.48, 0.85, 0.85, 0.92])

Like a post office box that is identified by a box number, an array element is identified by an index.