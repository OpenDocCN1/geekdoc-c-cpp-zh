# 8.1 Array Elements

An array is a simple but powerful programming language construct used to group and organize data. When writing a program that manages a large amount of information, such as a list of 100 names, it is not practical to declare separate variables for each piece of data. Arrays solve this problem by letting us declare one variable that can hold multiple, individually accessible values.

An array is a list of values. Each value is stored at a specific, numbered position in the array. The number corresponding to each position is called an index or a subscript. Figure 8.1 shows an array of integers and the indexes that correspond to each position. The array is called height; it contains integers that represent several peoples’ heights in inches.

In Java, array indexes always begin at zero. Therefore the value stored at index 5 is actually the sixth value in the array. The array shown in Figure 8.1 has 11 values, indexed from 0 to 10.

KEY CONCEPT
An array of size N is indexed from 0 to N-1.

To access a value in an array, we use the name of the array followed by the index in square brackets. For example, the following expression refers to the ninth value in the array height:

```
height[8]
```

According to Figure 8.1, height[8] (pronounced height-sub-eight) contains the value 79. Don’t confuse the value of the index, in this case 8, with the value stored in the array at that index, in this case 79.

![](bbox=[0.3, 0.75, 0.75, 0.9])

FIGURE 8.1 An array called height containing integer values